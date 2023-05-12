---
description: We use a combination of methods to let us monitor the health of our system.
---

# Runbook

### Alerting

tbd

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

TBD