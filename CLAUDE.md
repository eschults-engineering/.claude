<!-- Clone this repo as `.claude` in the folder that holds the org's repositories, e.g. ~/code/eschults-engineering/.claude. Claude Code loads it in every session started inside a sibling repo, before that repo's own CLAUDE.md. Repo-specific instructions belong in the repo, not here. -->

# eschults-engineering

## Git

- Commit messages are one line.
- Never commit to `master` or `main` without explicit permission; branch first.
- Never force-push, rebase, or amend a commit you did not write.
- PR descriptions have a Context section and a Changes section. No "Generated with Claude Code" line, no session URL.

## Prose

- No mid-sentence linebreaks in Markdown: READMEs, PR and issue descriptions, docs. One paragraph is one line, however long; the renderer wraps it.
- Plain, direct sentences. No filler, no hedging, no recap of what was just said.

## Pull Requests
- Title should be clear and concise (under 72 characters)
- Body should have two ## Context and ## Changes sections
- Context should be a concise explanation of the problem the PR is solving
- Changes should list the main changes, in a not-too-technical way
- Never insert "🤖 Generated with Claude Code"

## Code Comments

Write code that does not need one: a better name or a smaller method beats a comment. When one is unavoidable, make it a single line saying *why*, never what the line below already says.

Delete a comment when it repeats a test name, an assertion, or a `because:` sitting next to it, or when it narrates how a bug was found; that belongs in the commit and the PR.

Keep the ones whose loss would let a bug back in: a language or library trap, a constraint invisible from the call site, a decision that looks wrong until you know the reason.

Leave generated boilerplate alone; rewriting it only makes the next upgrade diff noisier.

## Tests

- Prove a new test bites: break the code it covers, watch it fail, restore. A test that has only ever passed has not been tested.
- Assert behaviour, not source text.
- Every bug fix ships with a regression test that fails before the fix and passes after it.
- Run the repo's full suite before opening a PR. Never mark a red run green.
