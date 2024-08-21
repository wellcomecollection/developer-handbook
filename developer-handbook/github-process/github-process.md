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
As a team, we operate in a very friendly, trusted, no-blame culture. The nature of code review can sometimes make this feel a little bit difficult, especially if you're a new joiner.

That's why we hope documenting our standards for both pull request and code review processes will help in strengthening our confidence and interpretation of them. We also hope it helps empower new joiners in tackling their first code reviews, or submitting their first feature.

We're approaching this from a place of believing code review to be an excellent a learning tool. Both for the submitter, who benefits from suggestions on their PR, but also for the reviewer. It's a prime place to ask questions, and learn from the submitter themselves.

So have a look through, and feel free to submit changes. In order:
- [Pull request creation](./pull-request-process.md)
- [Code review considerations](./code-review-process.md)
- [Post-code review process](./post-code-review.md)
