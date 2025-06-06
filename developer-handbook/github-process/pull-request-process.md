# Pull request creation

Here are recommendations to consider from the moment you create a new branch to work on.

## Pre-creation considerations

**Consider creating your Pull Request as soon as you can**

Consider creating your Pull Request as soon as possible. Think of PRs less as validation of work done and more as visibility of work in progress. The description ideally offers context as to why the work is being done as well as explaining how the solution was decided on, which can be very helpful to reviewers. Create it as a draft, so no one gets notified of every commit.

This will also let others gain some familiarity with the code changes, and might allow them to flag things in advance.

Another important aspect of this is that it ensures that the lottery factor isn't a problem; if you can't be the one to finish the work, others have eyes on it, and access to the latest code changes.

**Pull Requests should be small as possible**

If you're working on something big, consider splitting it in multiple PRs. If that's not possible, aim to split your commits logically, with meaningful commit messages.

**Address `TODO`s**

Avoid adding any `TODO` at all to `main`. If they aren't as urgent or related to the original ticket, they don't need to be addressed in your PR (and probably shouldn't be). Either:

* Create a ticket to do the work that can be prioritised. Then raise it in Slack if it's something to bring up to the next planning/ensure it's on the team's radar if it's a bigger piece of work. or
* Fix the issue before merging

Add a comment describing the peculiarity or optimisation for context for the next person to read without implying the next person should fix it. In this context, you could link to the GitHub issue.

If there are pre-existing `TODO`s in files, please check they have a ticket in the backlog, and therefore a chance to get addressed, then tidy it up (again, we're aiming to be rid of `TODO` comments in `main`, but comments to explain quirky looking logic can stay).

## Pull Request creation considerations

A pull request should have a clear description with:

* Linked ticket, which is where the context should live
* Changes made
* How to test
* Risks and plan to mitigate

If useful, leave comments throughout the code before making it "Ready for review", to add to the context of the changes. If they are important, or useful for future devs, it should be left as comments in the code instead.

To bring attention to anything important or special, you can also add formatted notices, such as tips and alerts by using [GitHub markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts).

Ask yourself:

* Would new tests be relevant? If so, add them:
  * Do they adequately reflect the questions asked in the ticket?
  * Do they cover appropriate boundary conditions? (tests tend to cover what you want to happen, but should also cover what happens when the input is "wrong")
  * Do the tests tell a story? Are they easily readable?
* Does any external documentation need updating based on your changes. If so, ensure you link to them in the description.
* Read file changes as if you were code reviewing a colleague; what would you point out if it was the other way around?

Once that's all done, and all automated tests have passed, then mark your PR as "Ready for review". That should automatically assign the `CODEOWNERS` team to the PR, but feel free to tag specific people as well.
