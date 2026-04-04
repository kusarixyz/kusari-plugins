---
allowed-tools: EnterWorktree, Bash(gh pr view:*), Bash(gh pr list:*), Bash(gh pr diff:*), Bash(git branch:*), Bash(git checkout:*)
description: Execute an implementation plan (or single step) in an isolated git worktree, with code review after each step
argument-hint: <plan-folder-or-step-file>
disable-model-invocation: false
---

Execute implementation steps in an isolated git worktree. After each step, review the changes. If given a plan folder, execute all steps sequentially. If given a single step file, execute only that step. Stop on any failure and surface it to the user.

## Input

The user provided: `$ARGUMENTS`

This is either a path to an implementation plan folder (containing `index.md` and `step-NN-*.md` files) or a path/filename of a single step file.

- If it is a full path, check if it is a directory or file.
- If it is just a name, search the current working directory and its subdirectories. If multiple matches are found, ask the user which one they mean. If no matches are found, tell the user and stop.
- If it is a directory, it must contain an `index.md` and at least one `step-NN-*.md` file. If not, tell the user and stop.
- If it is a file, locate its sibling `index.md` in the same directory.

## Setup

1. Read `index.md` (from the plan folder, or sibling to the step file).
2. Determine the step list:
   - **Folder input:** collect all `step-NN-*.md` files, sorted by step number.
   - **Single step input:** the list contains only that one step file.
3. Enter an isolated git worktree using the `EnterWorktree` tool with name `build/<plan-folder-name>` (or `build/<step-filename>` for single steps). This switches the session's working directory to the worktree. All subsequent work happens there automatically.

## Execution Loop

For each step in the step list, in order:

### Phase 1: Execute

Launch the `execute` agent. Pass it:
- The step file path
- The index file path

If the agent reports a failure after retries, stop the entire build and report the failure to the user. Include the step name, the failing command/test, and its output.

### Phase 2: Review

Launch the `review` agent. Pass it:
- The diff from Phase 1 (run `git diff` to collect it)
- The step file path
- The index file path

The agent returns a report table. Display the full table to the user exactly as returned. Do not stop the build based on issue scores. The user decides whether to act on any reported issues after the build completes.

### Phase 3: Stage

After the review report is shown to the user:

1. Stage all changes: `git add -A` in the worktree.
2. Commit with message: `build: step N - <step title>`.
3. Proceed to the next step.

## Completion

After all steps finish successfully:

1. Provide a build summary with:
   - Each step: name, type (scaffolding/code), test results (if code step), review outcome
   - A consolidated list of choices and assumptions made by agents across all steps. For each, state what the agent decided, why (if discernible), and which step it occurred in. This allows the user to course-correct anything that diverged from their intent.
2. Do not exit the worktree or merge the branch. The session remains in the worktree so the user can inspect, amend, or continue. The user decides what to do next.

## Constraints

- Stop the entire build on any unresolved failure. Do not skip steps.
- All work happens in the worktree (entered via `EnterWorktree`). Do not exit the worktree during or after the build.
