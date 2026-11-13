# Incident comms and escalation

This is our playbook for a major incident: an incident big enough that we need clear roles, regular updates to users and colleagues, and possibly help from a supplier. It builds on the [incident response process](incident-response-process.md), which still says what an incident is and how we work one in Slack. This page adds who does what when the incident is major, how often we tell people, where decisions are written down, and how to reach our suppliers.

Lines marked _To be agreed_ are decisions the team has not made yet. They are listed in [Open decisions](#open-decisions) and will be filled in as they are made. We exercise this playbook in a tabletop exercise, [platform#6875](https://github.com/wellcomecollection/platform/issues/6875), and change it from what we learn.

### Declaring a major incident

Start from the definition of an incident in the [incident response process](incident-response-process.md#whats-an-incident). An incident is major when _To be agreed: the criteria, for example how much of which service is unavailable and for how long_.

The criteria also need to say whether these count:

* an outage caused by a supplier, such as Digirati or Elastic
* an outage outside office hours (see [out-of-hours support](out-of-hours-support.md))
* an outage that recovers on its own before anyone responds

We have no severity scale today. _To be agreed: whether we adopt one, and how it maps to the impact field on Statuspage._

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
| People working the incident | #wc-incident-response | _To be agreed_ |
| Colleagues and stakeholders | #wc-digital-platform and the comms list (internal) | _To be agreed_ |
| The public | [status.wellcomecollection.org](https://status.wellcomecollection.org/) | _To be agreed_ |

The Statuspage bot reminds #wc-incident-response when an incident has been open for 3, 6 and 12 hours. Those reminders are a backstop for when updates have lapsed.

_To be agreed: message templates for the first update, progress updates and resolution._

The comms list is kept in Statuspage and Notion (internal).

### Decision log

Write down each decision as it is made: the time, what was decided, who decided it and why. This covers decisions such as taking a service offline, putting up the banner, escalating to a supplier, rolling back and declaring the incident resolved. The log is the starting point for the timeline in the retro.

_To be agreed: where the log lives, for example the incident thread in #wc-incident-response or a GitHub incident issue._

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

If Statuspage itself is unavailable, as it was during the AWS outage on 2025-10-20, we tell people by email instead. _To be agreed: the written fallback and who sends it._

#### Site banner

The site banner has Prismic and non-Prismic versions, switched with toggles. _To be agreed: who decides to put the banner up, and who puts it up._

### Escalating to suppliers

Contact names, account numbers and support plans go in a private page in [wellcomecollection/private](https://github.com/wellcomecollection/private) (private). _To be agreed: that page is not written yet._ Supplier contracts are held by Collection, not D&T.

| Supplier | What they run for us | How to escalate |
|---|---|---|
| Digirati | IIIF services | Raise it in #digirati first, then as a ticket in their Jira (WSUPP) when there is something for them to act on |
| Elastic | Elastic Cloud | Raise a severity 1 support ticket in the Elastic Cloud console or by email to support@elastic.co |
| Innovative | Sierra | We do not contact Innovative directly. Tell Collections Product, who raise it with Innovative. Sierra has no status page |
| Prismic | Content management | Watch [status.prismic.io](https://status.prismic.io). _To be agreed: a support route_ |
| AWS | Hosting | Check the AWS Health dashboard. Support plans differ between our accounts: see the private page |
| Auth0 | Sign-in | _To be agreed_ |

_To be agreed: the severity terms and response times each supplier offers, once someone has read the contracts._

Within the team, the people who escalate to suppliers are listed by role in the private page.

### D&T major incidents

D&T run their own Major Incident Management Process (internal) in ServiceNow, with a "P1 - Major Incident" Teams channel. We have no route into it today, and our services are not raised as D&T P1s. _To be agreed with D&T: whether that stays the case, or how we notify them_ ([platform#6797](https://github.com/wellcomecollection/platform/issues/6797)).

Security incidents go to the Head of Information Security, as the [incident response process](incident-response-process.md) and [bug nurse](bug-nurse.md#unexpected-security-events) pages say.

### Out of hours

Outside office hours, support is best effort, with the exceptions on the [out-of-hours support](out-of-hours-support.md) page. _To be agreed: whether one of those exceptions is declared as a major incident, and who is contacted._

### Closing the incident

The incident is resolved when the user-facing problem is fixed or mitigated as far as it can be. Today the delivery manager declares it resolved, as the [incident response process](incident-response-process.md#resolving-an-incident) says. _To be agreed: whether that holds for a major incident, and what else must be done before it is closed, for example the Statuspage incident resolved, the banner taken down, suppliers told and the decision log complete._

### Postmortem

After a major incident:

* Hold a retro, usually on the same or the next working day.
* Write it up in [docs/incident\_retros](https://github.com/wellcomecollection/docs/tree/main/incident_retros), following the layout of the existing write-ups: incident from and until, retro held, timeline, analysis of causes, and actions by owner.
* Link the write-up from the Statuspage incident as its postmortem update.
* Turn larger actions into GitHub issues.
* Keep findings that should not be public in a private write-up.

_To be agreed: whether every major incident gets a retro, a Statuspage entry and a GitHub incident issue._ Backplane (internal) is designed to count GitHub issues labelled `incident` in each service's change failure rate, though it does not read them yet.

### Escalation

* Not sure whether it is major? Ask in #wc-digital-platform rather than waiting.
* No response from the team? Go to the Digital Platform lead directly.
* A likely compromise or data exposure goes to the [incident response process](incident-response-process.md) and a private channel.

### Open decisions

* The criteria for a major incident, and whether supplier-caused, out-of-hours and self-recovering outages count
* Whether we adopt a severity scale, and how it maps to Statuspage impact
* How often to post updates for each audience, and the message templates
* Where the decision log lives
* The fallback when Statuspage is down
* Who decides on and puts up the site banner
* The Prismic and Auth0 escalation routes, the private supplier page, and supplier severity terms
* The boundary with the D&T major incident process
* How the out-of-hours exceptions relate to declaring a major incident
* Whether the delivery manager still declares resolution for a major incident, and what closing requires
* Whether every major incident gets a retro, a Statuspage entry and a GitHub issue

### Further reading

* [Incident response process](incident-response-process.md)
* [Bug nurse](bug-nurse.md)
* [Out-of-hours support](out-of-hours-support.md)
* [Write-ups of previous incidents](https://github.com/wellcomecollection/docs/tree/main/incident_retros)
