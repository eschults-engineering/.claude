---
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(gh pr create:*)
argument-hint: [branch-name]
description: Create logical git commits with 1-liner messages and PR with Context and Changes sections
---

## Task

Create logical git commits and a pull request with proper formatting based on the current changes.

## Current State

- Current branch: !`git branch --show-current`
- Git status: !`git status`
- Changes: !`git diff HEAD`
- Recent commits: !`git log --oneline -5`

## Your Workflow

1. **Analyze the changes** to identify logical units of work
2. **Create logical commits** following these rules:
   - Use concise 1-liner commit messages (under 72 characters)
   - Group related changes into separate commits
   - No attribution or co-author lines in commits

3. **Push the branch** to remote with `-u` flag

4. **Create a pull request** with this exact format:
   - **Title**: Clear, concise title (under 72 characters)
   - **Body**:
     ```
     ## Context
     [Brief explanation of why this change is needed, what problem it solves]

     ## Changes
     - [Bullet point describing change 1]
     - [Bullet point describing change 2]
     - [Bullet point describing change 3]
     ```

## Instructions

1. If `$ARGUMENTS` contains a branch name, create that branch first. Otherwise, verify we're not on `master`
2. Analyze all changes and group them logically
3. Stage and commit each logical group separately using: `git commit -m "concise message"`
4. Push the branch to remote
5. Create the PR using `gh pr create` with the proper format
6. Run `/review` on the new PR

Always ensure commits are atomic and the PR description clearly explains both context and changes.
