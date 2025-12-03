---
description: How we work with Feature Flags, which we call Toggles
---

# Toggles/Feature Flags

​[Technical README](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/toggles/README.md)

[Toggles dashboard](https://dash.wellcomecollection.org/toggles/)

​Feature flags (also known as feature toggles or feature switches) are a software development technique that turns certain functionality on and off during runtime, without deploying new code. This allows for better control and more experimentation over the full lifecycle of features.

In the Wellcome Collection team, we call them Toggles, and you can find them on our [Toggles dashboard](https://dash.wellcomecollection.org/toggles/). This dashboard is made available to anyone internal who it may help, and not just the digital team, so we try to ensure it's very clear.

We have **Permanent** and **Experimental** toggles, as you can see. Permanent ones, such as the API Toolbar, are features we want to keep for the long term, but not make publicly available. Usually they will be tools that are useful to the internal teams. The Experimental ones are usually more for works in progress.

Turning a toggle **ON** will make that feature available to **you only,** as it sets a cookie in your browser that our code looks for - so if you change browser or clear your cookies, you'll have to reselect it for the feature to be available. You can then turn it back **OFF** if you want to compare. The cookies work by default in both the prod and the staging environment, unless we specify otherwise. If any _are_ specified, they'll be in the "**Stage**" section on the dashboard.

We can share links that turn toggles on and off:

On: [https://dash.wellcomecollection.org/toggles/?enableToggle=newThemePages](https://dash.wellcomecollection.org/toggles/?enableToggle=newThemePages)&#x20;

Off: [https://dash.wellcomecollection.org/toggles/?disableToggle=newThemePages](https://dash.wellcomecollection.org/toggles/?disableToggle=newThemePages)

The id for the toggle can be found at [https://github.com/wellcomecollection/wellcomecollection.org/blob/main/toggles/webapp/toggles.ts](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/toggles/webapp/toggles.ts)&#x20;

We can run a script that turns these toggle **ON** for _the wider public_, which we'll usually do when the feature is ready for delivery\* but we still want to be able to turn it off quickly should anything go wrong, by rerunning the script and reverting its effect. You can find out their public status by looking here:

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7ftXlBv9uu465I0Z76rS%2Fuploads%2F4uDzHHKcVKxn6psoicWT%2Fimage.png?alt=media&#x26;token=f478b4c7-ec9b-43d2-be30-047ceebe0bf6" alt=""><figcaption><p>Public status is individual to each toggle</p></figcaption></figure>

**Stage** toggles, i.e. a toggle created with type 'stage', works as above, but they will only work on stage.

**Test** toggles are used, in conjunction with a [Lambda@Edge](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html), to facilitate A/B testing. Creating a toggle of type 'test' and adding it to the dashboard ensures that the status of the toggle gets sent to GA alongside event data (so we can analyse the impact of the toggled code) and allows people to opt in and out of the test. The [Lambda@Edge](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html) is used to split traffic 50/50 by setting a cookie value for the toggle automatically when web pages are viewed.

Steps to create an A/B test are available [here](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/cache/README.md#steps-to-create-an-ab-test).

\*Before turning a toggle ON (making it available to the wider public), we should make sure of a few things:

* [ ] Approved by PM
* [ ] Approved by any other internal stakeholder
* [ ] Approved by Design
* [ ] Analytics plan done and approved by Digital Analyst
* [ ] e2es have passed with this particular toggle turned on

Only once all these conditions are satisfied should we run the script.

### Note about 404 pages and toggles

A thing to note is **the yellow box on the 404 pages**. If you encounter a 404 page and have toggles enabled, it'll list which ones so you can try disabling them to see if it fixes it or not. It was added as it usually is an issue with the "Staging API" toggle, so make sure to confirm it's not what causes the issue.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F7ftXlBv9uu465I0Z76rS%2Fuploads%2FbQb8mGJEqbkpAUEAYPGE%2Fimage.png?alt=media&#x26;token=83e7c685-ff9c-4f6b-b53a-4823c0a40dc9" alt=""><figcaption><p>404 page with a yellow box indicating which toggles are active for the user</p></figcaption></figure>
