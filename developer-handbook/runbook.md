---
description: We use a combination of methods to let us monitor the health of our system.
---

# Runbook

### Alerting

Alerts appear in our Slack channel.

### Health and performance

The health and performance of our system is monitored by a number of dashboards.

* [Pa11y](https://dash.wellcomecollection.org/pa11y/report.latest.html)
* [Speedtracker](http://ghp.wellcomecollection.org/speedtracker/)
* [Datastudio](https://datastudio.google.com)
* Application bundle size
  * [Catalogue](https://dash.wellcomecollection.org/bundles/catalogue.browser.latest.html)

## Troubleshooting

We run on a **roll forward** methodology, trying to fix and improve the site rather than roll back.

However, if core functionality is at stake, **rolling back** is the quickest way to relieve pressure, so that we can roll forward.

### Rolling back

We can roll back to any Docker container we have built. You can find the Docker containers publicly hosted on [Docker Hub](https://hub.docker.com/r/wellcome/).

To roll back, find the docker container you need\*, then run `./deploy/terraform_deploy_service.sh <SERVICE_NAME> <DOCKER_CONTAINER_TAG>`.

Once rolled back, we can start diagnosing the problem.

\* The process here still needs work, as we have no way of indicating the last docker build we considered healthy.

### Diagnosing the problem

If the error was from CloudWatch, we store the logs locally in S3, go into Athena, and run the `ALB Logging - create` saved query, followed by `5xx errors` saved query. You should be able to spot the location of the error from there\*\*.

\*\* These should be saved in terraform, but currently aren't.

## Testing

### Updown.io

[Updown](https://updown.io/) is a tool that consistently monitors specified pages' availabilities and performances. [You may access our dashboard here](https://updown.io/p/1bj95). When a page goes down, an alert is sent in either #wc-platform-alerts or #wc-platform (or both), as well as emails to digital@.&#x20;

Devs can find more information in [the project's README file](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/updown/README.md), on how to add a page, which should be done when a new page type gets released.

### Cardigan/Storybook

[Our instance of Storybook is called Cardigan](https://cardigan.wellcomecollection.org/), the name tends to be used interchangeably in the team. It is used for two purposes; as a publicly accessible UI library, but also as a testing tool.&#x20;

Paired with [Chromatic](https://www.chromatic.com/) (a tool built by [Storybook](https://storybook.js.org/) maintainers), we get a build of Cardigan within every branch (that has an open PR). On each commit, Chromatic checks if there are visual differences between the old and new versions of each component, both on the desktop and mobile format. If any changes are found, they need to be approved by the dev, who will get an email alerting them to it.&#x20;

Those builds can also be used as a shareable link with the designer/anyone who would need to approve changes before a merge.

### Pa11y

[Pa11y](https://github.com/pa11y/pa11y) is a package we use for accessibility (a11y) purposes. On every deployment to production, [our dashboard ](https://dash.wellcomecollection.org/pa11y/)is updated with a report on pa11y's accessibility tests against specified pages (see our [README](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/pa11y/README.md) to learn how to add pages). A developer who adds a page type should ensure it's added to pa11y and the report comes back clean. Any new issues, at the time of writing, would be raised by the delivery manager on a daily basis.

### End-to-end tests&#x20;

We use [Playwright](https://playwright.dev/) for our e2es, and these run on deployments to staging and production, as well as an optional step in each PR. Three tests will run: Desktop tests, mobile tests and Check URL.

#### Desktop and mobile tests

These are the same test cases, which we code to account for both. [You may find them here](https://github.com/wellcomecollection/wellcomecollection.org/tree/main/playwright/test).\
These tests should test real-world case scenarios from beginning to end, these use cases having ideally been determined upon by a user researcher.

#### Check URL

Check Url (or url-checker)'s code [can be found here](https://github.com/wellcomecollection/wellcomecollection.org/tree/main/playwright/url-checker). It takes a list of pages and runs several tests against them to check on a few things, such as Javascript errors and requests failures. Any new page type should be added to the list so ensure we're monitoring it.&#x20;

### Unit/Integration testing

We use [react-testing-library's jest package](https://github.com/testing-library/jest-dom#readme) to run our unit and integration tests, which can be found in various places in the code and can be run with `yarn test:all:unit` at the root of the project. Some tests can be found within the component folder, or within the `test` folder that lives within the `common`, `content` and `identity` repositories.
