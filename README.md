# eschults-engineering/.claude

Claude Code rules and settings shared by every repository in the org. Claude Code has no org-level config of its own, so each repo pulls this in as a git submodule and links the rules into its own `.claude/rules/`.

## Install into a repo

From the root of the repository:

```sh
git submodule add git@github.com:eschults-engineering/.claude.git .claude/org
sh .claude/org/bin/install
```

The script symlinks `.claude/rules/org` to the submodule's `rules/` directory, so Claude Code loads every rule at session start, and copies `settings.json` to `.claude/settings.json` when the repo has none yet. If the repo already has one, merge by hand. Commit the result.

## Update a repo

```sh
git submodule update --remote .claude/org
```

Then commit the new submodule pointer.

## Layout

- `rules/` — one topic per file, loaded into every session of every repo that installed it. Keep each file short and concrete.
- `settings.json` — the baseline `.claude/settings.json`: permissions every repo should start from.
- `bin/install` — the install script above.

Repo-specific instructions stay in that repo's `CLAUDE.md`; only put here what should hold everywhere.
