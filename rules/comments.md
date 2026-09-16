# Comments

Write code that does not need one: a better name or a smaller method beats a comment. When one is unavoidable, make it a single line saying *why*, never what the line below already says.

Delete a comment when it repeats a test name, an assertion, or a `because:` sitting next to it, or when it narrates how a bug was found; that belongs in the commit and the PR.

Keep the ones whose loss would let a bug back in: a language or library trap, a constraint invisible from the call site, a decision that looks wrong until you know the reason.

Leave generated boilerplate alone; rewriting it only makes the next upgrade diff noisier.
