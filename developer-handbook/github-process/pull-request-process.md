# Pull Request creation

Here are recommendations to consider from the moment you create a new branch to work on.

## Pre-creation considerations

**Consider creating your Pull Request when you're 30-50% through**
_If it's a big piece_, consider creating your PR when you're 30-50% through. Create it as a draft, so no one gets notified of every commit. 

This will let others gain some familiarity with the code changes, and might allow them to flag things in advance. 

This also ensures that the lottery factor isn't a problem; if you can't be the one to finish the work, others have eyes on it.

**Pull Requests should be small as possible**
If you're working on something big, consider splitting it in multiple PRs. If that's not possible, aim to split your commits logically, with meaningful commit messages.

**Address `TODOs`**
If there are `TODO`s in the changed files, even if they were there before you started your work: it's your responsability to check they have a chance to get addressed. 

If they aren't as urgent or related to the original ticket, they don't need to be addressed in your PR (and probably shouldn't be). But every `TODO` should have a Github issue linked, so create one and add its link as a comment if it's not the case. Ensure it's on the team's radar if it's a bigger piece of work. 

## Pull Request creation considerations
A pull request should have a clear description with:
  - Linked ticket, which is where the context should live
  - Changes made
  - How to test
  - Risks and plan to mitigate

If useful, leave comments throughout the code before making it "Ready for review", to add to the context of the changes. If they are important, or useful for future devs, it should be left as comments in the code instead.

To bring attention to anything important or special, you can also add formatted notices, such as tips and alerts by using [GitHub markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts).

Ask yourself:
- Would new tests be relevant? If so, add them.
- Does any external documentation need updating based on your changes. If so, ensure you link to them in the description.
- If I code review myself, reading file changes as if you were code reviewing a colleague; what would you point out if it was the other way around? 

Once that's all done, and all automated tests have passed, then mark your PR as "Ready for review". That should automatically assign the CODEOWNER team to the PR, but feel free to tag specific people as well.