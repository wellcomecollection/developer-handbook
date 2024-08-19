# GitHub Process

See [How we work in Notion](https://www.notion.so/wellcometrust/How-we-work-8dc54e71aee345009dbea1e4fba577f5?pvs=4) for a view on team processes.

## Language used: Projects, Issues & Pull Requests (PRs)

Projects, Issues & PRs overlap in GitHub, here is how we think about them:

* Projects are quarterly iterations of the projects [available in Github](https://github.com/orgs/wellcomecollection/projects).
* Issues & PRs are both _change requests_.
* A PR is the unit of deployment, i.e. PRs should be deployable in isolation (where possible).
* PRs reference a set of git commits which in totality describe a coherent functional change.
* Issues reference one or more PRs which together describe a coherent functional change.
* Github Projects contain Issues _or_ PRs which transition through defined states towards _done_.

## Processes 
In order:
- [Pull request creation](./pull-request-process.md)
- [Code review considerations](./code-review-process.md)
- [Post-code review process](./post-code-review.md)
