# GitHub Process

See [How we work in Notion](https://www.notion.so/wellcometrust/How-we-work-8dc54e71aee345009dbea1e4fba577f5?pvs=4) for a view on team processes.

### Projects

Projects are quarterly iterations of the projects [available in Github](https://github.com/wellcometrust/platform/projects).

Issues are erased or recycled on a quarterly basis.

### Projects, Issues & Pull Requests (PRs)

Projects, Issues & PRs overlap in GitHub, here is how we think about them:

* Issues & PRs are both _change requests_.
* A PR is the unit of deployment, i.e. PRs should be deployable in isolation (where possible).
* PRs reference a set of git commits which in totality describe a coherent functional change.
* Issues reference one or more PRs which together describe a coherent functional change.
* Github Projects contain Issues _or_ PRs which transition through defined states towards _done_.

### Issue / PR requirements

All change requests should have in general:

* What is the benefit of this change (and for who) e.g. In order to make searches better for users
* What is the change functionally e.g. We've ordered searches by date
* What is the change: A brief overview of the implementation where useful e.g. This is an update to the `ElasticFlarp GargleMap` in `object FleebChunker`.
* Relationships to other changes e.g. Depends on #123, required for #456

For example:

```
In order to make searches better for users
We've ordered searches by date
By implementing an update to the `ElasticFlarp GargleMap` in `object FleebChunker`

Depends on #123, required for #456
```

### Definition of done

You do not need to enumerate these in pull requests, but you must be cognisant of them when closing PRs.

To be **done** they require:

* A code review from a non-pairing peer
* A deployment plan i.e. Code has been exercised in a production matching environment
* Testing as appropriate:
  * Acceptance criteria: high level testing functional change.
  * Regression testing (practically this probably means running the existing test suite)
  * Smoke tests (when this change is deployed - does the system it has been deployed to still function as expected)
* Documentation as appropriate
* Review with UX or Product as appropriate

PRs are merged by one of those who worked on the change.

Changes **should** be deployed immediately, or if they are not there **must** be a clear timescale indicated on the PR.
