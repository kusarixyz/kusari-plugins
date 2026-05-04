---
name: evaluate-skill
description: Test, measure, and iteratively improve Claude Code skills. Use when the user wants to test a skill, run evals, benchmark skill performance, compare two skill versions, optimize a skill's description for better triggering accuracy, or measure whether a skill provides value over baseline Also use when the user says "evaluate my skill", "test this skill", "is my skill working", "improve triggering", "compare these skills", or "run evals".
argument-hint: "[path-to-skill]"
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
---

# Evaluate Skill

When this skill is loaded, output exactly this block before any other response:

```
░█░█░█░█░█▀▀░█▀█░█▀▄░▀█▀░░░░░█▀▀░█░█░█▀█░█░░░█░█░█▀█░▀█▀░█▀▀
░█▀▄░█░█░▀▀█░█▀█░█▀▄░░█░░▄▄▄░█▀▀░▀▄▀░█▀█░█░░░█░█░█▀█░░█░░█▀▀
░▀░▀░▀▀▀░▀▀▀░▀░▀░▀░▀░▀▀▀░░░░░▀▀▀░░▀░░▀░▀░▀▀▀░▀▀▀░▀░▀░░▀░░▀▀▀
```

Test, measure, and iteratively improve Claude Code skills through structured evaluation.

## Phase 0: Detect and Route

### 0.1 Identify the skill under test

If `$ARGUMENTS` contains a path, use it. Otherwise check the current conversation for a skill path mentioned earlier. If neither, ask:

> Which skill do you want to evaluate? Provide the path to the skill directory.

Verify the path contains a SKILL.md. If not, stop.

### 0.1b Select model and effort

Ask the user which model and effort level to use for the evaluation runs:

> Which model should the eval runs use? (e.g. `sonnet`, `opus`, `haiku`, or a specific model ID)
>
> What effort level? (`low`, `medium`, `high`, `xhigh`, `max`, or skip for default)

Record both in `eval_metadata.json` and the report metadata. If the user skips effort, omit it (use the model's default).

**Every Agent tool call in Phase 2 (eval runners) and Phase 3 (grader, analyzer) MUST pass `model: "<selected-model>"` explicitly.** Subagents do not inherit the parent session's model. If you omit the model parameter, the subagent runs on the parent's model, defeating the purpose of model selection.

### 0.2 Detect existing workspace

The evaluation workspace lives at `<project-root>/evaluations/<skill-name>/`. Look for this directory. If it exists, check for `evals.json` and `iteration-*/` subdirectories.

| State | Signal |
|---|---|
| No workspace | First evaluation. Proceed to Phase 1. |
| Workspace with iterations | Prior work exists. Offer to continue from the latest iteration (skip to Phase 4 to review, or Phase 5 to improve) or start fresh. |
| Workspace with `feedback.json` in latest iteration | User reviewed but improvement not yet applied. Skip to Phase 5. |

### 0.3 Classify entry point

Determine intent from the user's request:

| Intent | Route |
|---|---|
| Test and evaluate a skill | Phase 1 |
| Continue iterating on prior results | Phase 4 or 5 (per 0.2) |
| Optimize description / fix triggering | Phase 6 |
| Compare two skill versions | Phase 1, with both versions as test targets |

### 0.4 Classify skill value type

Read the skill's SKILL.md and classify:

**Capability uplift** -- the skill teaches techniques the base model cannot reliably produce on its own. Testing must compare with-skill vs without-skill to prove the skill adds value. Examples: file format skills, API-specific knowledge, creative techniques.

**Encoded preference** -- the skill sequences steps the model can already handle individually. Testing focuses on whether the workflow produces consistent, correctly-ordered output. Baseline comparison is less meaningful since the model can do each step; the value is in the orchestration. Examples: debug workflows, planning procedures.

This classification affects how Phase 2 baselines are configured and how Phase 3 results are interpreted.

## Phase 1: Design Test Prompts

### 1.1 Create test prompts

Design 3-5 realistic test prompts. Each prompt should be something a real user would type, with enough specificity to produce a meaningful output.

Qualities of good test prompts:
- Concrete: include file paths, column names, personal context, specific details
- Varied: mix lengths, formality levels, edge cases
- Representative: cover the skill's core use cases and at least one boundary case

Bad: "Format this data"
Good: "I have a CSV in ~/reports/q4-sales.csv with columns for region, revenue, and headcount. Can you make a chart showing revenue per region?"

### 1.2 Classify test approach

Based on the skill value type from Phase 0.4:

| Value type | Baseline | What to measure |
|---|---|---|
| Capability uplift | Without skill (same prompt, no skill loaded) | Does the skill enable output the model cannot produce alone? |
| Encoded preference | Without skill, OR no baseline | Does the skill produce consistent, correctly-sequenced output? |

For capability uplift, always run a without-skill baseline. For encoded preference, a baseline is optional but useful for measuring consistency improvement.

### 1.3 Draft assertions

For each test prompt, draft 2-4 quantitative assertions. Assertions must be objectively verifiable.

Good assertions:
- "Output file exists and is valid XLSX" (programmatically checkable)
- "Chart contains exactly 3 data series" (inspectable)
- "Response includes SQL query before executing it" (pattern match)

Bad assertions:
- "Output looks professional" (subjective)
- "Code is well-structured" (unmeasurable)

### 1.4 Store fixture files

If a test prompt references input files (source code to review, configs to clean up, etc.), the fixtures MUST live at `<project-root>/evaluations/<skill-name>/references/`, next to evals.json. Never use `/tmp`, the user's home directory, or any other ad-hoc location: those paths are machine-specific, get wiped on reboot, and break reproducibility across iterations and contributors.

Create the `references/` directory if it does not exist. Mirror any logical grouping inside it (e.g. `references/imports/cart.ts`, `references/deletion/utils.ts`). Write the fixture file contents.

In evals.json, refer to fixtures with repo-relative paths starting at `evaluations/<skill-name>/references/...`. Use the same relative path in both the `prompt` text and the `files` array, so the eval subagent reads what the user-facing prompt describes. Eval subagents inherit the project-root cwd, so relative paths resolve correctly.

### 1.5 Save test cases

Check if `<project-root>/evaluations/<skill-name>/evals.json` already exists. If it does, read it and present the existing test cases to the user. Ask whether to use them as-is, modify them, or generate new ones.

If no evals.json exists, save to `<project-root>/evaluations/<skill-name>/evals.json`:

```json
{
  "skill_name": "example-skill",
  "evals": [
    {
      "id": 1,
      "prompt": "Review this file: evaluations/example-skill/references/sample.ts",
      "expected_output": "Description of expected result",
      "assertions": [
        "Output file exists at the specified path",
        "File contains at least 3 sections"
      ],
      "files": ["evaluations/example-skill/references/sample.ts"]
    }
  ]
}
```

Present the test prompts and assertions to the user for review before proceeding.

## Phase 2: Run Tests

### 2.1 Create workspace

Create `<project-root>/evaluations/<skill-name>/iteration-<N>-<model>-<effort>/` for the current iteration. If the user skipped effort, omit that segment: `iteration-<N>-<model>/`. Sanitize model and effort to lowercase with hyphens (e.g. `claude-opus-4-7`, `medium`). The evals.json lives at the skill-name level; iteration directories are nested under it.

If `<project-root>/evaluations/.gitignore` does not exist, create it with:

```
*
!.gitignore
```

This prevents eval outputs, logs, and grading results -- which may contain skill content, prompts, and Claude response data -- from being accidentally committed.

To pick `<N>`, scan existing `iteration-*/` directories, parse the integer immediately after `iteration-`, and use max+1 (or 1 if none exist).

### 2.2 Spawn all runs in one turn

For each test prompt, spawn two subagents in the same turn:

**With-skill run:**
```
Execute this task:
- Skill path: <path-to-skill>
- Task: <eval prompt>
- Input files: <eval files if any>
- Save outputs to: <iteration-dir>/eval-<ID>/with_skill/run-1/outputs/
```

**Baseline run** (for capability uplift skills):
```
Execute this task (no skill):
- Task: <eval prompt>
- Input files: <eval files if any>
- Save outputs to: <iteration-dir>/eval-<ID>/without_skill/run-1/outputs/
```

The `run-1/` subdirectory inside each config is required. The aggregation script scans for `run-*` directories to collect results. For multiple runs of the same eval, use `run-2/`, `run-3/`, etc.

Launch all runs (with-skill + baseline for every test case) in the same turn. Do not wait for with-skill runs to finish before spawning baselines.

Write an `eval_metadata.json` for each test case in the eval directory (not inside run-1/):
```json
{
  "eval_id": 0,
  "eval_name": "descriptive-name-here",
  "prompt": "The user's task prompt",
  "assertions": ["assertion 1", "assertion 2"],
  "model": "<model-id-powering-this-session>",
  "effort": "<effort-level-or-null>",
  "timestamp": "<ISO-8601 timestamp>"
}
```

### 2.3 Capture timing data

When each subagent task completes, the notification contains `total_tokens` and `duration_ms`. Save immediately to `timing.json` in the `run-1/` directory:

```json
{
  "total_tokens": 84852,
  "duration_ms": 23332,
  "total_duration_seconds": 23.3
}
```

This data is only available in the task notification. Capture it as each notification arrives.

## Phase 3: Grade and Benchmark

### 3.1 Grade each run

For each completed run, dispatch the grader agent (`${CLAUDE_SKILL_DIR}/agents/grader.md`). The grader evaluates every assertion against the outputs and saves `grading.json` in the `run-1/` directory (alongside `timing.json` and `outputs/`).

For assertions that can be checked programmatically (file exists, contains N items, matches pattern), write and run a script rather than relying on the grader's judgment. Scripts are faster, more reliable, and reusable across iterations.

The `grading.json` expectations array must use the fields `text`, `passed`, and `evidence`. The aggregation script depends on these exact field names.

### 3.2 Aggregate benchmark

Run the aggregation script:
```bash
python -m scripts.aggregate_benchmark <iteration-dir> --skill-name <name>
```

This produces `benchmark.json` with:
- Pass rate, time, and tokens for each configuration
- Mean, stddev, min, max per metric
- Delta between with-skill and baseline

### 3.3 Analyze patterns

Dispatch the analyzer agent (`${CLAUDE_SKILL_DIR}/agents/analyzer.md`) to read the benchmark data and surface patterns the aggregate stats might hide:
- Assertions that always pass regardless of skill (non-discriminating)
- High-variance evals (possibly flaky)
- Time/token tradeoffs
- Per-assertion and cross-eval patterns

The analyzer writes observations to `analysis.json` in the iteration directory.

## Phase 4: Review with User

### 4.1 Present results

The analyzer agent presents results directly to the user after writing `analysis.json`. If the user returns to review results from a previous iteration, read `analysis.json` and present the summary/overhead table, recommendations table, and detailed sections as described in the analyzer agent.

### 4.2 Collect feedback

Ask the user for feedback on the results. If they provide structured feedback, save it to `feedback.json` in the iteration directory.

Empty feedback on a test case means it looked fine. Focus improvement effort on test cases where the user has specific complaints.

If the user is satisfied with all results, the evaluation is complete. Otherwise, proceed to Phase 5.

## Phase 5: Improve and Iterate

### 5.1 Analyze feedback

Read the user's feedback alongside the grading results and analyzer observations. Identify:
- Which test cases failed or received negative feedback
- Whether failures are specific to individual cases or systemic
- Whether the skill's instructions caused the model to waste effort (read transcripts, not just outputs)

### 5.2 Improve the skill

Apply changes to the skill. Guidelines:

**Generalize, do not overfit.** The test cases are a sample. Changes that fix one test case but would break others are harmful. If a stubborn issue persists, try different approaches rather than adding rigid constraints.

**Keep the skill lean.** If the model wastes time on unproductive steps, remove the instructions causing it. Read the transcripts to identify these.

**Explain the why.** Constraints with rationale outperform constraints with emphasis. "NEVER do X because it causes Y" is stronger than "NEVER do X" alone.

**Look for repeated work.** If every test run independently wrote a similar helper script or took the same multi-step approach, the skill should bundle that script in scripts/.

### 5.3 Rerun

After improving the skill, return to Phase 2. Run all test cases into a new iteration directory with `<N>` incremented (model and effort segments may differ if the user selects different ones for this run).

For capability uplift skills, the baseline is always without-skill. For encoded preference skills, use judgment: baseline against the previous iteration or the original version.

### 5.4 Loop exit

Stop iterating when:
- The user says they are satisfied
- All assertions pass and feedback is empty
- Improvements are no longer producing meaningful change

## Phase 6: Description Optimization

This phase optimizes the skill's description for trigger accuracy. Accessible directly from Phase 0 when the user's goal is trigger improvement, or after Phase 5 when the skill content is stable.

Read `references/description-optimization.md` for the full methodology: designing trigger eval queries, the train/test split approach, running the optimization loop, and applying results.
