# Incident comms and escalation

This is our playbook for a major incident: an incident big enough that we need clear roles, regular updates to users and colleagues, and possibly help from a supplier. It builds on the [incident response process](incident-response-process.md), which still says what an incident is and how we work one in Slack. This page adds who does what when the incident is major, how often we tell people, where decisions are written down, and how to reach our suppliers.

We exercise this playbook in a tabletop exercise, [platform#6875](https://github.com/wellcomecollection/platform/issues/6875), and change it from what we learn.

### Declaring a major incident

Start from the definition of an incident in the [incident response process](incident-response-process.md#whats-an-incident). An incident is major when either of these is true:

* the website, search, the catalogue API, requesting or sign-in is unavailable or badly degraded for most users for 30 minutes or more
* there is a confirmed security or data exposure

It still counts when a supplier, such as Digirati or Elastic, is the cause.

We use two levels, "major incident" and "incident". On Statuspage, a major incident is a major or critical outage on the affected components, and an incident is degraded performance or a partial outage.

The delivery manager decides whether something is an incident, and anyone can start the process themselves as long as they tell the delivery manager. Either the incident lead or the delivery manager can declare a major incident, so one of them can do it when the other is away.

To declare, announce it in #wc-digital-platform, ask people to join #wc-incident-response, and fill in the roles below.

### Roles

| Role | What they do | Who takes it |
|---|---|---|
| Incident lead | Runs the incident: makes sure the other roles are filled, keeps the decision log, decides when to escalate to a supplier, and hands the role on explicitly if they step away | The most senior developer available |
| Technical lead | Works out what is wrong and how to fix or mitigate it, pulls in whoever they need, and posts progress in #wc-incident-response | Chosen by the incident lead |
| Comms lead | Opens and updates the Statuspage incident, keeps stakeholders informed, and decides on the site banner | The delivery manager, with the lead engineer as cover |

Supporting colleagues work as the [incident response process](incident-response-process.md#supporting-colleague) describes.

Which team owns each service is in its `manifest.yml`, which Backplane (internal) reads. Use it to find who to pull in rather than keeping a list here.

### Updates

| Audience | Where | How often |
|---|---|---|
| People working the incident | The incident thread in #wc-incident-response | Every 30 minutes |
| Colleagues and stakeholders | #wc-digital-platform and the comms list (internal) | When Statuspage is updated |
| The public | [status.wellcomecollection.org](https://status.wellcomecollection.org/) | At least every 60 minutes |

The Statuspage bot reminds #wc-incident-response when an incident has been open for 3, 6 and 12 hours. Those reminders are a backstop for when updates have lapsed.

Post the update on time even when nothing has changed. For example: "Search is still unavailable. We think the cause is the Elasticsearch cluster and are working with Elastic. Next update by 14:30."

The comms list is kept in Statuspage and Notion (internal).

### Decision log

Write down each decision as it is made: the time, what was decided, who decided it and why. This covers decisions such as taking a service offline, putting up the banner, escalating to a supplier, rolling back and declaring the incident resolved. The log is the starting point for the timeline in the retro.

The log lives in the incident thread in #wc-incident-response. Post each decision there starting with "Decision:", and copy them into the retro.

### Statuspage

The comms lead opens a Statuspage incident for every major incident that affects users.

Choose the affected components:

| Component | Covers |
|---|---|
| Collections Search | Collection search APIs and front-end |
| Requesting & Sign-in | Identity and library item requesting services |
| Image Services | IIIF Presentation and Image services |
| Website & Content | Front end and content services |

Move the incident through the states as it progresses:

* **Investigating** when we know something is wrong but not why
* **Identified** when we know the cause
* **Monitoring** when a fix or mitigation is in place and we are watching it
* **Resolved** when the user-facing problem is fixed or mitigated as far as it can be

Supplier-caused incidents get a Statuspage incident too, as the Digirati ones did in April and May 2026.

If Statuspage itself is unavailable, as it was during the AWS outage on 2025-10-20, the comms lead emails the stakeholder distribution list instead, and updates Statuspage once it is back.

#### Site banner

The site banner has Prismic and non-Prismic versions, switched with toggles. The comms lead decides whether to put it up. Anyone with Prismic editor access posts it, and the incident lead can post it if no editor is available.

### Escalating to suppliers

Contact names, account numbers and support plans are in the [supplier page](https://github.com/wellcomecollection/private/blob/main/suppliers.md) (private). Supplier contracts are held by Collection, not D&T.

| Supplier | What they run for us | How to escalate |
|---|---|---|
| Digirati | IIIF services | Raise it in #digirati first, then as a ticket in their Jira (WSUPP) when there is something for them to act on |
| Elastic | Elastic Cloud | Raise a severity 1 support ticket in the Elastic Cloud console or by email to support@elastic.co |
| Innovative | Sierra | We do not contact Innovative directly. Tell Collections Product, who raise it with Innovative. Sierra has no status page |
| Prismic | Content management | Check [status.prismic.io](https://status.prismic.io), then raise an issue on the Prismic support portal |
| AWS | Hosting | Check the AWS Health dashboard. Support plans differ between our accounts: see the supplier page |
| Auth0 | Sign-in | Check [status.auth0.com](https://status.auth0.com), then raise a case at [support.auth0.com](https://support.auth0.com) |

Within the team, the people who escalate to suppliers are listed by role in the supplier page.

### D&T major incidents

D&T run their own Major Incident Management Process (internal) in ServiceNow, with a "P1 - Major Incident" Teams channel. We run our own major incidents and don't raise them as D&T P1s ([platform#6797](https://github.com/wellcomecollection/platform/issues/6797)). The comms lead tells the D&T service desk when a major incident is declared and when it closes.

D&T take over only if the incident involves their systems or is a security incident. Security incidents follow the route in the [incident response process](incident-response-process.md#resolving-an-incident).

### Out of hours

Outside office hours, support is best effort, with the exceptions on the [out-of-hours support](out-of-hours-support.md) page. An exception that meets the criteria above is declared as a major incident.

### Closing the incident

The incident lead or the delivery manager closes a major incident once service has been restored and stable for 30 minutes. Every major incident gets a Statuspage entry, a GitHub issue labelled `incident`, and a retro written up in [docs/incident\_retros](https://github.com/wellcomecollection/docs/tree/main/incident_retros) within five working days.

### Postmortem

After a major incident:

* Hold a retro, usually on the same or the next working day.
* Write it up in [docs/incident\_retros](https://github.com/wellcomecollection/docs/tree/main/incident_retros), following the layout of the existing write-ups: incident from and until, retro held, timeline, analysis of causes, and actions by owner.
* Link the write-up from the Statuspage incident as its postmortem update.
* Turn larger actions into GitHub issues.
* Keep findings that should not be public in a private write-up.

Backplane (internal) is designed to count GitHub issues labelled `incident` in each service's change failure rate, though it does not read them yet.

### Escalation

* Not sure whether it is major? Ask in #wc-digital-platform rather than waiting.
* No response from the team? Go to the Digital Platform lead directly.
* A likely compromise or data exposure goes to the [incident response process](incident-response-process.md) and a private channel.

### Further reading

* [Incident response process](incident-response-process.md)
* [Bug nurse](bug-nurse.md)
* [Out-of-hours support](out-of-hours-support.md)
* [Write-ups of previous incidents](https://github.com/wellcomecollection/docs/tree/main/incident_retros)
