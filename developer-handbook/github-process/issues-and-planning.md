# Issues and planning

This page describes how the Digital Platform and Digital Experience teams record, plan and track work in GitHub. The two teams share a sprint rhythm and most of their conventions, and each section says where their practice differs.

## Where work lives

Platform work is recorded as issues in [wellcomecollection/platform](https://github.com/wellcomecollection/platform/issues), and Experience work as issues in [wellcomecollection.org](https://github.com/wellcomecollection/wellcomecollection.org/issues). Each team plans from its own board:

| Board | Used for |
|---|---|
| [Digital Platform](https://github.com/orgs/wellcomecollection/projects/17) | Platform work being considered, planned this quarter or in a sprint |
| [Digital Experience](https://github.com/orgs/wellcomecollection/projects/18) | Experience work from the icebox through refinement to done |
| [Platform health backlog](https://github.com/orgs/wellcomecollection/projects/19) | Long-running health work that is not tied to a quarter |

The boards are standing boards. Sprints are the iterations within them.

## Raising an issue

The platform repository has an issue form for each common kind of work. Choosing a form sets the issue type and any label for you.

| Form | Type | Label | Use it for |
|---|---|---|---|
| Task or improvement | Task | | Building, changing, upgrading or finding something out |
| Bug or data problem | Bug | `🐛 Bug` | Something behaves wrongly, or records or data are wrong |
| Planned change | Task | | An operational change done in steps, such as a switchover, reindex or decommission |
| Incident | Bug | `incident` | The record of a user-facing incident, opened during or after it |
| Retro action | Task | `retro-action` | An action agreed in an incident retro |
| Tracking issue | Epic | `Tracking Issue` | A larger piece of work split into sub-issues |

The wellcomecollection.org repository has its own templates for bug reports, feature requests, design briefs, feature QA, A/B tests and research. Issues raised from most of them are added to the Digital Experience board automatically.

Blank issues are still allowed for anything that does not fit a form. Do not open an issue for a security problem or an exposed secret; use a private channel and the [incident response process](../../incident-management/incident-response-process.md). If something is down now, follow the [major incident playbook](../../incident-management/incident-comms-and-escalation.md) first and open the incident issue once the incident is under way.

## Larger pieces of work

On Platform, a larger piece of work is a tracking issue, with the Epic type and the `Tracking Issue` label. Each slice of the work is a sub-issue rather than a line in a checklist, so progress shows on the issue and on the board. The sub-issues are estimated and the tracking issue is not. A tracking issue closes when its "Done when" is met, which may be more than every sub-issue being closed.

On Experience, a larger piece of work is usually a user story with the Feature type, broken into sub-issues as the work becomes clear. Related stories are grouped with an `epic:` label.

The two teams put the estimate in different places. Platform estimates the sub-issues, and Experience estimates the user story.

## Intake and triage

Requests and reports from colleagues come in through #wc-platform-feedback, and alerts arrive in #wc-platform-alerts. The [bug nurse](../../incident-management/bug-nurse.md) for the week triages both and raises an issue when work is needed, usually with the bug, task or planned change form.

What happens to a new issue is decided by the delivery manager, the technical product manager and the developers together. It goes into Next or a sprint on the Digital Platform board, onto the Platform health backlog, or it is closed. The Digital Experience board works the same way, with the product manager taking the technical product manager's part. Requests that cross between the teams are decided the same way.

## Priority and capacity

Work is prioritised first by how well it fits the quarter's objectives. Within that, alerts are handled by their severity as the [alert routing ADR](https://github.com/wellcomecollection/docs/blob/main/adr/alert_routing.md) sets out, and vulnerabilities and incidents follow the rules on the [bug nurse page](../../incident-management/bug-nurse.md) and in the [major incident playbook](../../incident-management/incident-comms-and-escalation.md). After that, work follows the order and dates of its milestones.

Sprint planning aims at the team's running average of points per sprint, which the delivery manager works out from recent sprints.

## Sprints and boards

Both teams run two-week sprints that start on a Wednesday, six to a quarter. The last sprint of a quarter can be short, and a firebreak week follows the quarter.

The teams hold a daily stand-up and plan at the start of each sprint. Platform holds a retro in the week between plannings, and every fourth week the retro is a joint one with Experience. The two teams also hold a joint technical review every fortnight and a Show and Tell for colleagues every five or six weeks.

### Digital Platform board

The Status column moves left to right:

| Status | Meaning |
|---|---|
| No status | Considered, not yet planned |
| Next | Planned for this quarter |
| A column per open sprint, such as "Q1 sprint 5 25 November" | Committed to that sprint |
| In progress | Being worked on |
| Ready for review | Waiting for review |
| Blocked | Waiting on something outside the team's control |
| Done | Finished this sprint |
| Archive | Moved out of Done once the sprint summary has been written |

Committed work also has its Sprint iteration set. Engineers estimate in Fibonacci points at planning, in the board's Estimate field rather than the issue body.

At the end of a sprint, work in progress keeps its status and gains the new sprint. Work that has not started moves to the new sprint's column. Finished work is closed and keeps the sprint it was finished in.

Each sprint has an overview issue labelled `🏁 Sprint Overview` at the top of its column, titled "Sprint N (Qn yy/yy): goal". Work the team will pick up only if there is time carries the `:shipit: stretch` label.

### Digital Experience board

The Status column runs Icebox, Backlog, Ready for refinement, Sprint ready, a column for the current sprint named by its start date, In progress, Ready for review, Blocked, Done and Archive. The board has no Sprint iteration field, so the sprint column is the commitment.

The product manager leads a backlog refinement session each fortnight with the senior developers and the delivery manager, where user stories are estimated and moved to Sprint ready.

The Digital Experience team's ways of working are in Notion (internal):

* [Planning](https://www.notion.so/wellcometrust/Planning-66afb8e41b084a90838fa53722e20e77) (internal)
* [Sprint plans](https://www.notion.so/wellcometrust/Sprint-plans-54f9c0b1759c49d8b2a3ff1ba25b1db3) (internal)
* [QA](https://www.notion.so/wellcometrust/QA-1766687658a180c996c7f91a6913cfb2) (internal)
* [Allocating assignees and reviewers](https://www.notion.so/wellcometrust/Allocating-assignees-and-reviewers-2486687658a1807e8d12c1e44efaadb0) (internal)

## Quarterly objectives

Each team sets objectives and key results each quarter, and they are reviewed at the quarterly D&T OKR sessions. Quarterly planning turns them into milestones and issues. An issue connects to an objective through its milestone, and a tracking issue can name the objective in its Links field.

At the end of each sprint the delivery manager sends colleagues a one-page summary of what was done, grouped by objective.

The Digital Platform sprint process is written up in the planning repository's [sprints README](https://github.com/wellcomecollection/digital-platform-planning-delivery/blob/main/sprints/README.md) (internal).

## Recurring reviews

Some reviews are part of the planning rhythm:

* The lead engineer reviews the standard change catalogue every quarter, as the [change model ADR](https://github.com/wellcomecollection/docs/blob/main/adr/change_model.md) describes.
* The lead engineers review service ownership every quarter and record the review as an issue on the Digital Platform board, as the [service ownership ADR](https://github.com/wellcomecollection/docs/blob/main/adr/service_ownership.md) describes.
* Alerts that arrived over the weekend are reviewed each Monday, as the [alert routing ADR](https://github.com/wellcomecollection/docs/blob/main/adr/alert_routing.md) describes.
* Each sprint, a vulnerabilities lead from the Digital Platform team picks up vulnerabilities that owning teams have not fixed, as the [bug nurse page](../../incident-management/bug-nurse.md) describes.
