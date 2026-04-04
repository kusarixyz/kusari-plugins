---
allowed-tools: Bash(git add:*), Bash(git commit:*), Bash(git checkout:*), Bash(git merge:*), Bash(git branch:*), Bash(git log:*), Bash(git diff:*), Bash(git status), Bash(git push:*), Bash(git worktree:*), ExitWorktree
description: Stage, commit, merge the build branch, and clean up the worktree
argument-hint: "[step-title]"
disable-model-invocation: false
---

Finalize a build step by committing, merging, and cleaning up the worktree.

## Input

The user provided: `$ARGUMENTS`

This is an optional argument. If provided, it is the build step title (e.g., "step 1 - project scaffolding"). If not provided, scan the current conversation for a prior `/build` or `/execute` invocation. If one is found, derive the step title from the most recent step that was executed. If none are found, derive the title from the current branch name.

## Steps

1. Run `git status` to check for uncommitted changes.
2. If there are uncommitted changes:
   - Stage all changes: `git add -A`.
   - Commit with message: `build: <step-title>` and a one-line summary of what was implemented, derived from the diff.
3. If the working tree is clean, skip to step 4. The build command may have already committed.
4. Record the current branch name (the build branch).
5. Exit the worktree using `ExitWorktree` with action `keep`. You cannot checkout the base branch from inside the worktree because the base branch is already checked out by the parent repo.
6. Now in the original directory, merge the build branch: `git merge <build-branch>`.
7. If the merge fails, report the conflict to the user and stop. The worktree is still available for inspection.
8. If the step belongs to a plan (an `index.md` file exists as a sibling to the step file), mark the step as done in `index.md`. Find the line referencing the step, add a `[done]` tag, and apply strikethrough to the step title (e.g., `- ~~Step 1 - Project scaffolding~~ [done]`).
9. If the merge succeeds:
   - Push to remote: `git push`.
   - Remove the worktree: `git worktree remove <worktree-path>`.
   - Delete the build branch: `git branch -d <build-branch>`.

## Constraints

- Only push, remove the worktree, and delete the branch after a successful merge. If anything fails, stop and report.
