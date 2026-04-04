# kusari-dev

PRD-to-code pipeline. Plan implementation from a PRD, then execute steps with test-first development and automatic validation.

## Commands

### /plan

```
/plan <path-or-filename>
```

Translates a PRD into a step-by-step implementation plan. Argument is a PRD file path or filename.

Two-phase process:

1. **prd-analyzer** (cyan) -- Reads the PRD, identifies gaps and ambiguities, asks you to resolve them. Produces a structured analysis and proposed step breakdown.
2. **implementation-writer** (green) -- Translates the analysis into detailed implementation steps with interfaces, function signatures, test plans, and acceptance criteria.

Output for plans with 8 or fewer steps: a single `<prd-name>-implementation.md` file. For more than 8 steps: a directory with `index.md` skeleton and individual `step-NN-<name>.md` files.

### /execute

```
/execute <path-or-filename>
```

Launches the `execute` agent to run a single implementation plan step. Argument is a step file path or filename (e.g., `step-03-sqlite-database.md`).

### /review

```
/review [step-file]
```

Launches the `review` agent to review uncommitted changes. Runs parallel review agents to check for bugs, CLAUDE.md compliance, historical context, prior PR comments, and code comment adherence. Each finding is scored 0-100 and all issues are reported regardless of score.

Optional argument: a step file path or filename. When provided, an additional agent checks the diff against the step specification for missing functionality, contradictions, and out-of-scope changes. If omitted, infers the step file from a prior `/build` or `/execute` invocation in the conversation.

### /build

```
/build <plan-folder-or-step-file>
```

Executes implementation steps in an isolated git worktree (via `EnterWorktree`) with automatic code review after each step. Accepts either a plan folder (executes all steps sequentially) or a single step file.

For each step:
1. Launches the `execute` agent.
2. Launches the `review` agent (displays the full report table).
3. Commits on success, stops the entire build on failure.

After all steps complete, reports a consolidated summary of all choices and assumptions made by agents. The session remains in the worktree for inspection.

### /finish

```
/finish [step-title]
```

Finalizes a build step. Stages and commits any uncommitted changes, exits the worktree, merges the build branch into the base branch, pushes to remote, and cleans up the worktree and branch. If the step belongs to a plan, marks it as done in `index.md` with strikethrough.

Step title is optional. If omitted, inferred from a prior `/build` or `/execute` invocation or the current branch name.

### /evaluate

```
/evaluate <idea description or file path>
```

Evaluates a business idea, product plan, or feature through a panel of seven investor personas running in parallel. Each persona applies a distinct investment philosophy and returns a structured assessment.

Argument is either inline text describing the idea or a path to a file containing it. Before launching the panel, the command checks for missing context (stage, constraints, target market) and asks in a single batch.

Investor personas:

| Persona | Core Lens |
|---------|-----------|
| Paul Graham | Founder quality, organic demand, simplicity |
| Peter Thiel | Monopoly, contrarian truth, definite plan |
| Sam Altman | Scale ceiling, ambition, timing |
| Marc Andreessen | Market size, distribution, technology waves |
| Naval Ravikant | Leverage, specific knowledge, permissionless scale |
| Balaji Srinivasan | Regulatory risk, tech curves, global-first |
| Patrick Collison | Infrastructure, developer experience, patience |

Each investor returns: verdict (invest/pass/conditional), conviction level, bull case, bear case, key question, lens-specific question, and advice. The command then synthesizes a unified report with a verdicts table, consensus analysis, recurring risks, key questions, and an integrated assessment.

## Components

| Type | Name | Used by | Purpose |
|------|------|---------|---------|
| Command | plan | /plan | Orchestrates PRD-to-plan pipeline |
| Command | execute | /execute | Thin wrapper, launches execute agent |
| Command | review | /review | Thin wrapper, launches review agent |
| Command | build | /build | Executes plan in worktree with per-step review |
| Command | finish | /finish | Commits, merges, pushes, cleans up worktree |
| Command | evaluate | /evaluate | Orchestrates investor panel evaluation |
| Agent | prd-analyzer | /plan | Interrogates PRD for completeness |
| Agent | implementation-writer | /plan | Produces detailed step files |
| Agent | execute | /execute, /build | Orchestrates test-first step execution |
| Agent | review | /review, /build | Orchestrates multi-agent diff review |
| Agent | test-writer | execute agent | Writes tests before code |
| Agent | implementer | execute agent | Writes production code or scaffolding |
| Agent | investor-graham | /evaluate | Paul Graham persona |
| Agent | investor-thiel | /evaluate | Peter Thiel persona |
| Agent | investor-altman | /evaluate | Sam Altman persona |
| Agent | investor-andreessen | /evaluate | Marc Andreessen persona |
| Agent | investor-naval | /evaluate | Naval Ravikant persona |
| Agent | investor-balaji | /evaluate | Balaji Srinivasan persona |
| Agent | investor-collison | /evaluate | Patrick Collison persona |
