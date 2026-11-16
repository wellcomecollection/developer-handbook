# Rolling back a change

This page is how to undo a production change that has gone wrong. The usual rollback is a revert that goes through the same route as the original change. The [change model ADR](https://github.com/wellcomecollection/docs/blob/main/adr/change_model.md) and the [change model](change-model.md) page describe that route. If the change has caused a user-facing problem, follow the [incident response process](../incident-management/incident-response-process.md) as well.

### Watch your change after merge

Once you merge, keep an eye on the builds and tests in Buildkite until your change reaches production, and make any failure a priority. If something fails, say so in Slack so others hold their deploys, for example "My end-to-end failed in staging so please hold, I'm looking into it and might have to revert". The [post-code review](github-process/post-code-review.md) page has more on this.

### How each repository reaches production

At a gate, a person checks staging before approving the production deploy. In a repository with no gate a bad change reaches production with nothing to stop it, so watch the deploy and be ready to revert.

| Repository | Gate before production |
|---|---|
| wellcomecollection.org | Buildkite block "Allow prod deployment?": check the change and the main landing pages on staging |
| catalogue-api | Buildkite block "Deploy to prod?": check staging and the diff tool. The Identifiers API deploys through a GitHub environment that needs approval from the digital-platform team |
| identity | Buildkite block "deploy to prod": check staging |
| content-api | Buildkite block before the API deploy. The content pipeline, unpublisher and Prismic webhook lambdas deploy straight from `main` with no gate |
| storage-service | None. A merge deploys to stage, sends a test bag through stage, then triggers the production deploy |
| catalogue-pipeline | None. A merge triggers the adapter and pipeline deploys |
| platform-infrastructure | None. GitHub Actions deploys on push to `main`. Some lambdas in other accounts are still deployed with `terraform apply` |
| buildkite-infrastructure | None. CI checks formatting only, and Terraform is applied by hand |

### Application code

1. Open the merged pull request on GitHub and use its **Revert** button. This raises a revert pull request that links back to the original.
2. Take the revert through the normal route: review, CI, staging, then the production gate.
3. If the revert can't wait for review, it is an emergency change, and only the people named under [emergency changes](change-model.md#emergency-changes) can merge it without one.

`yarn deploy-dev restore content` (or `identity`) in wellcomecollection.org puts staging back after a dev deploy. It does not touch production.

Some changes can't be reverted, such as a data or index change, or a change on the pipeline side that the API depends on. Then fix forward with a new pull request through the same route, and say in the original pull request what you did.

### Toggles

A public toggle is switched back with the same command that switched it on, as the [toggles README](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/toggles/README.md) describes:

* a feature flag: `yarn setDefaultValueFor --TOGGLE_ID=false`
* a phased flag: `yarn setDefaultValueFor --TOGGLE_ID=null` makes no phase public

This changes production straight away, with no pull request.

### Terraform

Reverting the code on `main` doesn't change anything in AWS until someone applies it. Terraform is applied to production only from `main` after the pull request has merged, so to put the infrastructure back:

1. Raise a revert pull request for the original change, get it reviewed and merge it.
2. On an up-to-date `main`, run `terraform plan` and check that it reverses what the change did and nothing else.
3. Run `terraform apply`.

If users are affected and the revert can't wait for review, applying the commit on `main` from before the change is an emergency change. Only the lead engineer or a delegated senior engineer does it, and records it in #wc-digital-platform (see the [change model](change-model.md#emergency-changes)). Raise the revert pull request straight afterwards, so that `main` matches what is applied and the next apply from `main` doesn't put the change back.

The [2025-04-10 retro](https://github.com/wellcomecollection/docs/blob/main/incident_retros/2025-04-10_digital_assets_not_available.md) is an example: the plan from the earlier commit showed the same resources the morning's change had created and changed, and applying it fixed the problem.

Re-applying an earlier commit won't bring back the data in a resource that was destroyed, or a key or secret that was rotated. Say in the pull request how you would recover from a change like that before you apply it.

### Further reading

* [Change model](change-model.md)
* [Change model ADR](https://github.com/wellcomecollection/docs/blob/main/adr/change_model.md)
* [Post-code review process](github-process/post-code-review.md)
* [Incident response process](../incident-management/incident-response-process.md)
* [Write-ups of previous incidents](https://github.com/wellcomecollection/docs/tree/main/incident_retros)
