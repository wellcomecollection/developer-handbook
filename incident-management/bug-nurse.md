# Bug nurse

The bug nurse is the person from the Digital Platform or Digital Experience team who watches our alert and feedback channels for the week and makes sure each item reaches someone who will act on it. They do not have to fix everything themselves, but each alert should end up acknowledged and either handled, handed to its owner or ticketed.

### Who is on the rota

Names and dates are on the Slack canvas "Bug nurse / vulnerabilities", linked from the topic of #wc-platform-alerts. One or two people cover each week, and a Slackbot reminder in #wc-digital-general names them on Mondays. Each sprint, one of them also takes the vulnerabilities day (see [The vulnerabilities day](#the-vulnerabilities-day)).

### Daily duties

Do this each working morning, and look in again during the day.

| Channel | What to look at | Done means |
|---|---|---|
| #wc-platform-security-alerts | The GitHub security digest (07:30 weekdays) and the Inspector digest (07:31 weekdays) | Each new critical has an emoji; anything that needs work has an owner or a ticket |
| #wc-platform-security-alerts | Real-time Inspector criticals (they start with `:rotating_light:`) | The owning team has seen it, or you have started the fix |
| #wc-platform-security-alerts | Secret scanning alerts, posted within 15 minutes | The secret is revoked or rotated, then removed from the code (see [Same-day work](#same-day-work)) |
| #wc-platform-security-alerts | GuardDuty, IAM change and `admin/` secret access alerts | Someone has confirmed in the thread that it was expected (see [Unexpected security events](#unexpected-security-events)) |
| #wc-platform-alerts | Alarms, DLQ and Lambda errors, failed pipelines | Each alert is acknowledged and either explained, fixed or ticketed |
| #wc-platform-feedback | Feedback from users and colleagues | Each thread has a reply, and a GitHub issue where there is work to do |

On Mondays, also check the Inspector digest for criticals marked overdue and for anything owned by Digirati, and follow them up (see [Findings owned by Digirati](#findings-owned-by-digirati)).

### Emoji

React to each alert so others can see where it stands without reading the thread:

* :eyes: (`eyes`) when you are looking at it
* :white\_check\_mark: (`white_check_mark`) when it is handled, or ticketed with the issue linked in the thread
* :recycle: (`recycle`) when it is a repeat of something already known, with a link to the earlier thread or issue

### How quickly to fix vulnerabilities

The D&T Vulnerability Management Standard sets these timescales, counted from the date a vulnerability is classified. The [Inspector README](https://github.com/wellcomecollection/platform-infrastructure/blob/main/inspector/README.md#dt-standards-and-processes) links it and D&T's other vulnerability and incident documents.

| Severity | Fix within |
|---|---|
| Critical | 7 days |
| High | 14 days |
| Medium | 60 days |
| Low | 90 days |

Severity starts from the CVSS score (9.0 and above is critical, 7.0 to 8.9 high), but you can raise or lower it for our context, for example when the vulnerable code never runs or the resource is not reachable from the internet. Record the reason in the ticket or thread. The Inspector digest shows how long each critical has been open and marks it overdue after 14 days, so check criticals against the 7-day limit yourself.

#### Same-day work

Two kinds of alert are fixed or handed over on the day they arrive:

* An exploitable critical on a deployed resource, which is what the real-time Inspector alerts are. Start the rebuild or redeploy, or hand it to the owning team named in the alert and agree who does it.
* An exposed secret. Revoke or rotate it first, then remove it from the code. Treat a secret that was public as compromised and follow the [incident response process](incident-response-process.md).

### Unexpected security events

GuardDuty findings, changes to our standard IAM roles, new IAM users or access keys, and reads of `admin/` secrets are often someone doing their job. Ask in the alert's thread whether it was expected, and tag the person if CloudTrail names them.

If nobody confirms it on the same day, or it looks like a compromise, raise it in #wc-digital-platform and follow the [incident response process](incident-response-process.md). If nobody on the team picks it up, go to the Digital Platform lead directly. Discuss a suspected security incident in a private channel, and report it to the Head of Information Security, as that page says. Information Security then handle it under D&T's incident response plan, which the [Inspector README](https://github.com/wellcomecollection/platform-infrastructure/blob/main/inspector/README.md#dt-standards-and-processes) links. Security is one of the exceptions in [out-of-hours support](out-of-hours-support.md).

### Findings owned by Digirati

Digirati run our IIIF services, some of them in their own AWS account. The real-time alerts say "Owned by Digirati, who run it" for a finding that only runs in their account, and the digest lists their criticals after ours. Raise these in #digirati with a link to the digest thread, and follow up on any that pass their timescale. Where a fix depends on Digirati and cannot be made in time, record it as an exception through a suppression rule (see below), naming the compensating control.

### The vulnerabilities day

One day each sprint goes on vulnerabilities, as a child issue of wellcomecollection/platform#5796 assigned to that sprint's bug nurse. On that day:

* Work through open Dependabot alerts and PRs, and the Inspector highs in the daily report.
* Review the Inspector suppression rules and accepted risks whose review date falls in the sprint.
* Raise PRs or rebuilds for what can be fixed, and tickets for what cannot be done in the day.

#### Suppression rules and exceptions

Inspector suppression rules are how we record accepted risks and exceptions to the timescales above. They live in `inspector-filters-wellcome-collection.tf` in [wellcometrust/ncw-control-tower](https://github.com/wellcometrust/ncw-control-tower), and each one gives its review date in its reason.

A reviewed PR to that repository is the approval for an exception. Raise it before the timescale for the finding runs out, with a D&T Service Now request (D&T Requests, Cloud group) so NCW review and apply it. The PR description states:

* the CVE and its severity
* the affected systems
* why we are accepting the risk rather than fixing it
* the compensating controls
* a review date no more than a year away, which the rule's reason repeats

When a rule's review date comes round, either renew it with a new PR that restates the above, or remove it so the findings show again. Never add a rule to quieten findings nobody has looked at. The [Inspector README](https://github.com/wellcomecollection/platform-infrastructure/blob/main/inspector/README.md#suppression-rules) has the details of how rules are written and planned.

### Escalation

* Tag the owning team named in the alert, or raise it in #wc-digital-platform if there is none.
* If you are unsure whether something is serious, ask in #wc-digital-platform rather than waiting.
* A likely compromise or data exposure goes to the [incident response process](incident-response-process.md).

### Further reading

* [Amazon Inspector](https://github.com/wellcomecollection/platform-infrastructure/blob/main/inspector/README.md): how findings are scanned, routed and owned
* [security\_digest](https://github.com/wellcomecollection/platform-infrastructure/blob/main/monitoring/security_digest/README.md): what each digest and alert contains
* [Security alerts](https://github.com/wellcomecollection/platform-infrastructure/blob/main/monitoring/README.md#security-alerts): the GuardDuty, IAM and secret access rules
* [Dependabot](../developer-handbook/dependabot.md)
