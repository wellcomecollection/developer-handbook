# Dependabot

### What is Dependabot?

Automated dependency updates built into GitHub

### What do we use it for?

Keeping our repository safe and secure by making sure the modules that we use are up to date

### How does it work?

Following the configuration that we have set up in `[PROJECT_ROOT]/.github/dependabot.yml`, dependabot will run through the package.json files in our repositories, and check to see if there's an updated version of the package. If there is, it will create a pull request for the update.

### What is in the Pull Request?

The pull request if composed of these parts:

* the version jump
* if the source repository has it,
  * a link to the changelog
  * a snippet of the changelog messages of all the changes that have occured in between the releases (there is limited space, so this section may be truncated)
* All of the commits from the release in the package.json up until the latest release, and a link to the compare view of the changes

### What if I don't want to accept that update in time?

That's fine, dependabot will also periodically perform rebases when there are changes to the main branch. You can also manually trigger a rebase by commenting `@dependabot rebase`

### What if I don't want to interact with this package updates at all until there's a major update?

there are also multiple commands available to dependabot that, like the command above, to interact with dependabot and send it instructions, for how it should behave moving forward with that package.

You can trigger Dependabot actions by commenting on the PR:

* `@dependabot rebase` will rebase this PR
* `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
* `@dependabot merge` will merge this PR after your CI passes on it
* `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
* `@dependabot cancel merge` will cancel a previously requested merge and block automerging
* `@dependabot reopen` will reopen this PR if it is closed
* `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
* `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
* `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
* `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

### I want to make changes to the configuration file

that's fine! In fact, we've already covered the location of the configuration file! `[PROJECT_ROOT]/.github/dependabot.yml` if you would like to make any changes to it, please refer to the documentation that's found [here](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuration-options-for-the-dependabot.yml-file)
