# Out-of-hours support

As a general rule, we support Wellcome Collection services during UK office hours (9am to 5pm on weekdays). Outside those hours, support is best effort. If a service goes down on a Sunday morning, it may stay down until we arrive in the office on Monday.

This is a deliberate position, and the Head of Digital Experience and Engagement has accepted the risk that comes with it. The [service levels ADR](https://github.com/wellcomecollection/docs/blob/main/adr/service_levels.md) records it alongside our other service levels.

## Exceptions to this rule

We may make specific exceptions for certain classes of incident, such as incidents which incur a substantial risk if left unresolved. This may include:

* A significant **security or privacy** risk, e.g. if private data about library patrons becomes available publicly.
* A significant **financial** risk, e.g. if our AWS account is compromised and somebody tries to do expensive cryptocurrency mining on our dime.
* A significant **reputational** risk, e.g. if somebody vandalises the public website.

If the incident cannot be resolved quickly and safely, we should **take the affected services offline** until the next working day. More people will be around to help fix the problem, and there'll be less pressure on whoever is working out-of-hours.
