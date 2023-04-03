# When something goes bang

When there's a significant user-facing problem (e.g. a website outage), we want to fix it quickly.

The exact process will vary from incident-to-incident, but here are some guidelines for how we approach incidents:

1. We discuss ongoing incidents in the **#wc-incident-response channel** in Slack. This channel is only used for incident discussions; it doesn't have other topics or automated alerts that could interrupt the conversation.
2. **Post regularly** in the channel about what you're doing to help resolve the incident – this helps reduce duplication of effort and often makes debugging faster. It also helps us construct a timeline later.
3. We don't have hard-and-fast rules about whether incidents should be fixed by rolling back/forward – it varies by incident. Choose whatever's most appropriate to this problem.
4. After the incident is resolved, we usually hold an **incident retro** to discuss it. This starts with establishing a timeline (which is why posting in Slack is useful), understanding the cause(s) of the problem, and identifying any actions to take/changes to make to prevent a similar incident occurring in future.

{% hint style="warning" %}
If the incident is security-related (e.g. user data being leaked), discuss it in a private Slack channel rather than #wc-incident-response, which is public.

Any security incidents should be reported to the Head of Information Security.
{% endhint %}

### See also

* [Incident retrospectives](http://localhost:5000/s/7ftXlBv9uu465I0Z76rS/planning#incident-retrospectives) in "How we work"
* Our [write-ups of previous incidents](https://github.com/wellcomecollection/docs/tree/main/incident\_retros) on GitHub
