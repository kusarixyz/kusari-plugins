---
allowed-tools: EnterWorktree, Read, Glob, Grep, Bash, Agent
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
3. Enter an isolated git worktree using the `EnterWorktree` tool with name `build/<plan-folder-name>` (or `build/<step-filename>` for single steps). This switches the session's working directory to the worktree. All subsequent work happens there automatically. **Record the worktree absolute path** -- you will pass it to every spawned agent.
4. Read the agent definition files that will be used to launch sub-agents. These are at absolute paths under the plugin root `${CLAUDE_PLUGIN_ROOT}`:
   - `${CLAUDE_PLUGIN_ROOT}/agents/implementer.md` (always)
   - `${CLAUDE_PLUGIN_ROOT}/agents/test-writer.md` (always)
   - `${CLAUDE_PLUGIN_ROOT}/agents/test-reviewer.md` (for code steps)
   - `${CLAUDE_PLUGIN_ROOT}/agents/review.md` (always)
   - `${CLAUDE_PLUGIN_ROOT}/agents/maintainability-reviewer.md` (always, used by review agent)
   - `${CLAUDE_PLUGIN_ROOT}/agents/typescript-reviewer.md` (used by review agent if project is TypeScript)

## Execution Loop

For each step in the step list, in order:

### Phase 1: Execute

#### Step type detection

Detect the step type by checking for the classification tag in `index.md`: `[scaffolding]` or `[code]`. If neither tag is present, classify based on content: if the step has no Interfaces and no Functions/Methods sections (or they say "None"), it is scaffolding. Otherwise, it is code.

#### Scaffolding steps

1. Launch an agent using the contents of `agents/implementer.md` as its prompt. Append to the prompt:
   - The step file contents
   - The index file contents
   - Step type: "scaffolding"

2. After the implementer finishes, run the Post-Setup Verification commands listed in the step file. Run each command and check the output against the expected result described in the step.

3. If any verification command fails, launch the implementer agent again with the failure output and ask it to fix. Retry up to 3 times total.

4. Record the verification command outcomes.

#### Code steps

1. Launch an agent using the contents of `agents/test-writer.md` as its prompt. Append to the prompt:
   - The step file contents
   - The index file contents

2. After test-writer finishes, launch an agent using the contents of `agents/test-reviewer.md` as its prompt. Pass it the test files written in step 1 (collect via `git diff --name-only` filtered to test files). The test-reviewer returns findings as JSON.

3. If the test-reviewer returns findings, launch the test-writer agent again with the findings and ask it to fix the issues. Then re-run the test-reviewer. Repeat this review/fix cycle up to 3 times total. If findings remain after 3 cycles, report them to the user but proceed -- the tests exist, they just have quality issues the user can address later.

4. After test review is clean (or retries exhausted), launch an agent using the contents of `agents/implementer.md` as its prompt. Append to the prompt:
   - The step file contents
   - The index file contents
   - Step type: "code"

5. After the implementer finishes, detect the project's test runner and run the tests.

6. If tests fail, launch the implementer agent again with the failure output (stderr and stdout) and ask it to fix the production code. Do not modify test files. Retry up to 3 times total.

7. After exhausting retries with tests still failing, stop the entire build and report the failure to the user. Include the step name, the failing command/test, and its output.

8. Record what was implemented, test results (pass/fail counts), and the Acceptance Criteria from the step file as a checklist.

### Phase 2: Review

Launch an agent using the contents of `agents/review.md` as its prompt. Pass it:
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

- Use the `Write` tool to create new files and the `Edit` tool to modify existing files. Never use `Bash` with cat, echo, heredocs, or redirects to write or append to files. Reserve `Bash` exclusively for running commands (build, test, verification).
- Never skip the test-writer for code steps. Tests are written first, always.
- Never modify test files during the retry loop. Only production code gets fixed.
- The implementer must not add functionality beyond what the step specifies.
- Stop the entire build on any unresolved failure. Do not skip steps.
- All work happens in the worktree (entered via `EnterWorktree`). Do not exit the worktree during or after the build.
- Never stash, discard, reset, or modify uncommitted changes in the base branch. Those changes belong to the user and exist outside the scope of the build.
