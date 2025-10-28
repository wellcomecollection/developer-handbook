# Playwright NodeJS updates

When we update NodeJS in the `/playwright` directory, we need to use a version that is also supported by the latest [Docker image provided by Microsoft](https://playwright.dev/docs/docker). Similarly, we need to make sure that if we update the version of Playwright referenced in `/playwright/package.json` (e.g. as a result of a dependabot vulnerability alert), we should be sure to update to the same version in the Docker image.
