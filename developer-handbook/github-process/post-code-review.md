# Post Code Review

Your Pull Request was reviewed by a colleague (or a few colleagues, which is great). What's left to do now is

## Address it
- The "keep your comments friendly" rule applies here too! We all have the best intentions for our codebases.
- React or reply to every comment that was left, even if it's just "acknowledged" or "done", or an emoji reaction. The person that left it thought it was worth saying something, it's nice to acknowledge it.
- If some comments/suggestions need more discussion, switch to Slack or a call, but ensure you document the outcome in the PR for legacy's sake.
- Create new tickets if a piece has been suggested that isn't a blocker for release, and link to it in the PR comments for decision documentation.

## Post merge
- Keep an eye on the builds and tests running in Buildkite, make it a priority to address any fails. Flag in appropriate channels, for example: "My end-to-end failed in staging so please hold, I'm looking into it and might have to revert".
- If it's all good, ensure your code gets to production ASAP in order to avoid creating a backlog of commits.