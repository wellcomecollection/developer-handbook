---
description: >-
  Instructions for updating Node versions for apps in the wellcomecollection.org
  repo
---

# NodeJS updates

We aim to stay up-to-date with the most recent ('active') LTS (long-term support) version of Node wherever possible.

1. Choose the Active LTS NodeJS version from the [release schedule](https://nodejs.org/en/about/previous-releases)
2. Choose an appropriate Docker image running this version of Node – `bookworm-slim` is probably a good choice because `bookworm` means it will run likely run on a supported version of Debian until at least 2028 and `slim` means it contains everything required for a functional Node environment and nothing else
3. Change this Docker version in the appropriate `Dockerfile`(s)
4. Look in `.github/workflows` to see if any Node versions are referenced there which need updating
5. Change your local version of Node to the one you want to target (using `nvm` or similar)
6. Update the `.nvmrc` at the relevant level of the repo to the version you want to target (this will allow future repo users to [automatically choose the correct Node version](https://github.com/nvm-sh/nvm?tab=readme-ov-file#calling-nvm-use-automatically-in-a-directory-with-a-nvmrc-file)).&#x20;
7. Run `yarn` to update dependencies with the relevant Node version
8. Fix any dependency errors that might have resulted from the previous step
9. Run the app(s) locally, run any tests, and run any scripts in `package.json` to verify things work as expected
10. `cd` to the relevant `Dockerfile` directory and run `docker-compose build appNameGoesHere` then `docker-compose run -p 3000:3000 appNameGoesHere` (note there are extra steps required for the identity app as noted in the [README](https://github.com/wellcomecollection/wellcomecollection.org/blob/main/identity/README.md#local-development)) then verify things work as expected
11. Consider this an opportunity to upgrade packages that support the new version of Node so they don’t fall behind. It doesn’t need to be done in the same PR, but should be considered as a second step
12. Create PR including clear description of steps for how to run and test for reviewers. For side-apps (e.g. `dash` and `pa11y`) consider adding their build jobs to `.buildkite/pipeline.yml` to test the build on there. This can then be used as proof it should work. If you do this, remember to remove it before merging

