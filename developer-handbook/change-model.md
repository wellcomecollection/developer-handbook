# Change model

This page is how to make a production change day to day. The [change model ADR](https://github.com/wellcomecollection/docs/blob/main/adr/change_model.md) is the decision behind it: which routes a change can take, which record is the change record, and who holds change authority. It covers production changes to the services the digital platform team runs in the Wellcome Collection AWS accounts, including application code, Terraform and toggles.

Lines marked _To be agreed_ are decisions the team has not made yet. They are listed in [Open decisions](#open-decisions).

### Kinds of change

Every production change is one of three kinds. The names come from ITIL, the service management framework D&T used when they assessed us.

| Kind | What it means | How to tell |
|---|---|---|
| Normal | The usual route: a reviewed pull request, CI, a check on staging and an approved production deploy | It is not a standard or an emergency change. Most changes are normal |
| Standard | A kind of change we have agreed in advance is low risk, with a written procedure to follow | It matches an entry in the [standard changes](#standard-changes) table |
| Emergency | A change that can't wait for the normal route, made only by the lead engineer or a senior engineer they have delegated to | Waiting for review and a staging check would leave users affected for longer, usually during an incident |

### Making a normal change

Most changes take this route:

1. Open a pull request against `main` and fill in the headings of the pull request template.
2. Get an approving review from someone other than you. Branch protection asks for one, and CODEOWNERS requests it from the owning team.
3. Merge once CI has passed. Merging deploys to staging, where the service has one.
4. Check the change on staging.
5. Approve the production deploy at the Buildkite block step, or in the GitHub environment where the repository uses one.
6. Watch the deploy through to production, and be ready to revert (see [Rolling back a change](rollback.md)).

Some repositories have no staging environment, or go to production without a person checking staging first. [Rolling back a change](rollback.md#how-each-repository-reaches-production) lists which.

The merged pull request together with the GitHub Deployment that shipped it is the change record.

### Standard changes

A standard change is a kind of change we have agreed in advance is low risk and has a written procedure. Say in the pull request which entry it falls under, and get an approving review from someone other than you as usual. The catalogue is in the [ADR](https://github.com/wellcomecollection/docs/blob/main/adr/change_model.md#standard-changes), and today it has five entries:

| Change | Procedure |
|---|---|
| A dependency update raised by Dependabot, with CI passing | [Dependabot](dependabot.md) |
| Turning a toggle on for the public once its checklist is complete | [Toggles and feature flags](front-end/toggles-feature-flags.md#before-turning-a-toggle-on) |
| Updating a WAF IP list, either through the WAF IP set updaters or by adding an address to a block list | [WAF IP set updaters](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/cache/ip-updaters/README.md), and "Bot or scraper traffic slows or breaks the site" in the [website runbook](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/content/docs/runbook.md#bot-or-scraper-traffic-slows-or-breaks-the-site) |
| Changing an ECS service's task count or an Elastic Cloud deployment's size within agreed bounds | The bounds are recorded in the service's runbook. _To be written: the bounds for each service._ |
| Publishing a Prismic content model change in the documented order | [Updating an existing custom type](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/prismic-model/README.md#updating-an-existing-custom-type) in the prismic-model README |

To add or remove an entry, raise a pull request to the ADR. The lead engineer reviews the catalogue every quarter.

### Turning on a front-end feature

Before you make a toggle public, complete the checklist on the [toggles page](front-end/toggles-feature-flags.md#before-turning-a-toggle-on):

* approved by the PM
* approved by any other internal stakeholder
* approved by Design
* analytics plan done and approved by the Digital Analyst
* e2es have passed with the toggle turned on

Then run `yarn setDefaultValueFor --TOGGLE_ID=true`, as the [toggles README](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/toggles/README.md) describes. This changes what the public sees straight away, with no pull request. _To be agreed: where a public toggle change or a block list update is recorded._

### Emergency changes

An emergency change is one that can't wait for the normal route. Only the lead engineer, or a senior engineer the lead engineer has delegated authority to, makes one.

* Record the change in #wc-digital-platform when you make it, in one message per change that links the pull request or the Terraform apply.
* Merging without an approving review is not standard practice. Only the lead engineer does it, when it is required, and records it each time: say in the pull request body why it could not wait for review, and link the pull request in a message in #wc-digital-platform.
* Fill in the pull request template headings afterwards.

If you are not the lead engineer or a delegated senior engineer and something needs fixing now, follow the [incident response process](../incident-management/incident-response-process.md) and find one of them.

### Terraform

Any developer who has completed induction may run `terraform apply` against production. The Terraform code goes through the normal route like any other change. CloudTrail in each account is the record of who applied a change and when. Its coverage of every account is being confirmed with the D&T Cloud team under [platform#6793](https://github.com/wellcomecollection/platform/issues/6793).

* Apply to production only from `main`, after the pull request has merged. Applying from a branch, or from an older commit, is an emergency change.
* Read the whole plan before you apply, and check it changes only what you expect. A breaking change buried in a long plan caused the [2025-11-20 incident](https://github.com/wellcomecollection/docs/blob/main/incident_retros/2025-11-20_cannot_search_works_and_images.md).

To undo an apply, see [Rolling back a change](rollback.md#terraform).

### Fridays and bank holidays

We try not to make risky changes on a Friday or ahead of a bank holiday weekend. This is an informal habit. It is not written down as a rule, and we have no formal change freeze (see [End-of-year closure](../end-of-year-closure.md)). It comes from two incidents. The [2024-05-13 retro](https://github.com/wellcomecollection/docs/blob/main/incident_retros/2024-05-13_prismic_slice_machine_migration.md) recorded a decision not to make changes ahead of a bank holiday weekend, and the [2026-06-05 retro](https://github.com/wellcomecollection/docs/blob/main/incident_retros/2026-06-05_registration.md) said the change should not have been made on a Friday.

_To be agreed: whether this becomes a written rule, and if so what counts as risky._

### Where changes are counted

Backplane (internal), our developer portal, reports change failure rate from production deploys recorded as GitHub Deployments, and reads who owns each service from its `manifest.yml`. Look there rather than keeping a list here. Terraform applies, and deploys from repositories that don't create GitHub Deployments, are not counted.

### Open decisions

* Where a public toggle change or a block list update is recorded
* Whether the Friday and bank holiday habit becomes a written rule

### Further reading

* [Change model ADR](https://github.com/wellcomecollection/docs/blob/main/adr/change_model.md)
* [Rolling back a change](rollback.md)
* [Pull request creation](github-process/pull-request-process.md)
* [Post-code review process](github-process/post-code-review.md)
* [Toggles and feature flags](front-end/toggles-feature-flags.md)
