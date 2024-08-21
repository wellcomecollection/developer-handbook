# Code review

You've been assigned a Pull Request to review, and you want to get started. 

- The tone we go for is a friendly one; we all know we are reviewing the code and not the coder, but the lines are easily blurred (for example, try not to use words like "simply", "easily", "just", "obviously", "well, actually...").

- Code review is as much a priority as writing code is, so ensure you code review promptly to unblock your colleagues: make it part of your routine. For example, you could have a look at [the PR listing page](https://github.com/pulls/review-requested) in the morning, or in between pieces of work, to see if anything needs reviewing. If you can't find time, try to set a time aside in the future and let your colleagues know when that will be.

- If it's a huge PR, consider doing it in bits instead of in one go, it will be more efficient for your focus. Take your time!

- Don't be afraid to ask questions! It's a prime place to learn, and it might mean that the code could be more readable, or use comments.

- If a comment is not a blocker for release, make sure you state that by prefixing it with "Nit Pick".

- Don't be a perfectionist, but keep an eye out for:
	- Our own chosen standards (naming conventions, file structure, etc.)
	- Readability
	- Compliance (e.g. a11y)
	- Dead code
	- Performance concerns
	- Security concerns
	- Gaps in logic (e.g. in an `if` statement, is every case covered?)
	- Duplication of code (e.g. helpers that we already have a library for)
	- Edge cases
	- Leftovers from development, (e.g. `console.log`, addressed `TODO`s)
	- Typos!

- Ensure you follow the "How to test" section, and run your own tests on top of it if you can think of other useful ones.

- If you see something cool, or a nice detail, point it out. Positive comments on a PR are always appreciated.

- If the review becomes more of a conversation, ensure you get back to it promptly when new commits are submitted. 

- Use "Request changes" sparingly. We don't really want to use it, but if you think the PR contains security gaps, for example, it might be best to flag it as a change request.

- Final approval message should contain information on what was tested and how.