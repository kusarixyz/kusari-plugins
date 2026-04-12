---
repository: anthropics/skills
branch: main
skill-path: skills/skill-creator
analyzed: 2026-04-11
---

# Skill Analysis: skill-creator


## 1. Overview

**Skill name:** `skill-creator`

**Title text:** `Skill Creator`  
**Title char length:** 13

**Description (from YAML frontmatter):**
> Create new skills, modify and improve existing skills, and measure skill performance. Use when users want to create a skill from scratch, edit, or optimize an existing skill, run evals to test a skill, benchmark skill performance with variance analysis, or optimize a skill's description for better triggering accuracy.

**Description char length:** 318

**Total files (recursive):** 16

**Subdirectories:** 5 (`agents/`, `assets/`, `eval-viewer/`, `references/`, `scripts/`)

**Complete file list:**

| Path | Type | Size (bytes) |
|------|------|-------------|
| `LICENSE.txt` | file | 11,357 |
| `SKILL.md` | file | 33,168 |
| `agents/analyzer.md` | file | 10,376 |
| `agents/comparator.md` | file | 7,287 |
| `agents/grader.md` | file | 9,049 |
| `assets/eval_review.html` | file | 7,058 |
| `eval-viewer/generate_review.py` | file | 16,365 |
| `eval-viewer/viewer.html` | file | 44,998 |
| `references/schemas.md` | file | 12,061 |
| `scripts/__init__.py` | file | 0 |
| `scripts/aggregate_benchmark.py` | file | 14,386 |
| `scripts/generate_report.py` | file | 12,847 |
| `scripts/improve_description.py` | file | 11,116 |
| `scripts/package_skill.py` | file | 4,234 |
| `scripts/quick_validate.py` | file | 3,972 |
| `scripts/run_eval.py` | file | 11,464 |
| `scripts/run_loop.py` | file | 13,605 |
| `scripts/utils.py` | file | 1,661 |

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Line count | 486 |
| Word count | ~4,720 (estimated from content density) |
| Estimated token count (words / 0.75) | ~6,293 |
| Character count | 33,168 (per GitHub API size field) |

The file is the largest SKILL.md in the repository by byte count. At 486 lines it falls just under the skill's own recommended 500-line limit for SKILL.md files, a constraint the file explicitly states.

---

## 3. Document Structure Depth

### Heading list (with level and line numbers)

| Line | Level | Text |
|------|-------|------|
| 6 | H1 | `Skill Creator` |
| 32 | H2 | `Communicating with the user` |
| 45 | H2 | `Creating a skill` |
| 47 | H3 | `Capture Intent` |
| 57 | H3 | `Interview and Research` |
| 62 | H3 | `Write the SKILL.md` |
| 71 | H3 | `Skill Writing Guide` |
| 73 | H4 | `Anatomy of a Skill` |
| 87 | H4 | `Progressive Disclosure` |
| 100 | H4 | `Domain organization` |
| 111 | H4 | `Principle of Lack of Surprise` |
| 115 | H4 | `Writing Patterns` |
| 129 | H4 | `Examples pattern` (within `Writing Patterns` section — note: this is a bold `**Examples pattern**` inline, not a true heading; the actual H3 follows) |
| 137 | H3 | `Writing Style` |
| 141 | H3 | `Test Cases` |
| 163 | H2 | `Running and evaluating test cases` |
| 168 | H3 | `Step 1: Spawn all runs (with-skill AND baseline) in the same turn` |
| 199 | H3 | `Step 2: While runs are in progress, draft assertions` |
| 207 | H3 | `Step 3: As runs complete, capture timing data` |
| 221 | H3 | `Step 4: Grade, aggregate, and launch the viewer` |
| 253 | H3 | `What the user sees in the viewer` |
| 267 | H3 | `Step 5: Read the feedback` |
| 292 | H2 | `Improving the skill` |
| 295 | H3 | `How to think about improvements` |
| 309 | H3 | `The iteration loop` |
| 325 | H2 | `Advanced: Blind comparison` |
| 331 | H2 | `Description Optimization` |
| 336 | H3 | `Step 1: Generate trigger eval queries` |
| 362 | H3 | `Step 2: Review with user` |
| 373 | H3 | `Step 3: Run the optimization loop` |
| 396 | H3 | `How skill triggering works` |
| 402 | H3 | `Step 4: Apply the result` |
| 406 | H2 | `Package and Present (only if present_files tool is available)` |
| 419 | H2 | `Claude.ai-specific instructions` |
| 443 | H2 | `Cowork-Specific Instructions` |
| 458 | H2 | `Reference files` |

### Summary

| Level | Count |
|-------|-------|
| H1 | 1 |
| H2 | 11 |
| H3 | 19 |
| H4 | 6 |
| **Total headings** | **37** |

**Max heading depth:** H4 (4 levels)

---

## 4. Content Specificity Assessment

**Score: 5 / 5**

This is a maximally operational skill document. Nearly every sentence is an instruction, constraint, schema, or command invocation. Abstract guidance is consistently grounded with concrete code or examples immediately following.

**Justification excerpts:**

1. **Explicit shell command with arguments and flags** (line 229):
   ```bash
   python -m scripts.aggregate_benchmark <workspace>/iteration-N --skill-name <name>
   ```
   This is not advisory; it is the literal command to run. The surrounding text specifies what `<workspace>` and `<name>` refer to.

2. **Exact JSON schema for `eval_metadata.json`** (lines 190-197):
   ```json
   {
     "eval_id": 0,
     "eval_name": "descriptive-name-here",
     "prompt": "The user's task prompt",
     "assertions": []
   }
   ```
   The skill prescribes the exact field names and types, not a general description of what to store.

3. **Concrete positive/negative example contrast for trigger eval queries** (lines 350-357): The skill does not say "make realistic queries." It provides a labeled bad example (`"Format this data"`) and a labeled good example with file paths, column names, and backstory embedded in a first-person voice (`"ok so my boss just sent me this xlsx file..."`). This removes interpretation entirely.

---

## 5. Internal File References

Every file or path reference found in SKILL.md:

| Reference | Line(s) | Context | Exists in repo |
|-----------|---------|---------|----------------|
| `eval-viewer/generate_review.py` | 17, 239, 249 | Script to launch the review viewer; run with `nohup python` | Yes |
| `evals/evals.json` | 145, 161, 205 | Where test cases are saved; schema sourced from `references/schemas.md` | Not present in repo (created at runtime in skill workspace) |
| `references/schemas.md` | 161, 231 | Full JSON schemas for evals.json and benchmark.json | Yes |
| `agents/grader.md` | 225, 463 | Grader subagent instructions | Yes |
| `agents/comparator.md` | 327, 464 | Blind comparator subagent instructions | Yes |
| `agents/analyzer.md` | 234, 327, 465 | Post-hoc analyzer / benchmark analyzer subagent | Yes |
| `assets/eval_review.html` | 364 | HTML template for trigger eval query review UI | Yes |
| `scripts/run_loop.py` | 383 (via `-m scripts.run_loop`) | Description optimization loop script | Yes |
| `scripts/package_skill.py` | 412 (via `-m scripts.package_skill`) | Packages skill into `.skill` file | Yes |
| `scripts/aggregate_benchmark.py` | 229 (via `-m scripts.aggregate_benchmark`) | Aggregates benchmark results | Yes |
| `<workspace>/iteration-N/benchmark.json` | 229, 244 | Runtime output; path pattern, not a static file | N/A (runtime) |
| `/tmp/eval_review_<skill-name>.html` | 369 | Temp write location for eval_review.html | N/A (runtime) |
| `~/Downloads/eval_set.json` | 371 | Download destination for exported eval set | N/A (runtime) |
| `feedback.json` | 270, 284 | User review feedback output from viewer | N/A (runtime) |
| `timing.json` | 211, 216 | Per-run timing data file | N/A (runtime) |
| `eval_metadata.json` | 188, 196 | Per-eval metadata written during runs | N/A (runtime) |

**Summary:** All static references (agents, scripts, references, assets) resolve to files that exist in the repository. Runtime path patterns do not resolve statically by design.

---

## 6. Skill Cross-References

The SKILL.md contains no explicit references to other skills in the `anthropics/skills` repository by name. There is one indirect reference:

- Line 165: `"Do NOT use /skill-test or any other testing skill."` — a negative constraint that implies the existence of a `skill-test` skill or command but does not link to it. This is a prohibition, not a dependency.

No `skill:` URIs, skill names, or `skills/` directory paths pointing to sibling skills appear in the document.

---

## 7. Agent References

The SKILL.md explicitly references three agents, all located in `agents/`:

| Agent file | Lines referenced | Role |
|-----------|-----------------|------|
| `agents/grader.md` | 225, 463 | Evaluates assertions against execution transcripts and outputs; produces `grading.json` |
| `agents/comparator.md` | 327, 464 | Blind A/B comparator; judges output quality without knowing which skill produced which output |
| `agents/analyzer.md` | 234, 327, 465 | Two distinct roles: (1) post-hoc analysis of why the blind-comparison winner won; (2) benchmark pattern analysis across multiple runs |

The `agents/` directory contains exactly these three files and no others.

**Usage pattern:** The SKILL.md does not inline agent content; it defers with "Read `agents/grader.md`" when spawning that subagent. The Reference files section (lines 461-466) consolidates all agent references in one place as a directory.

---

## 8. Other Markdown File Analysis

### `agents/analyzer.md`

| Metric | Value |
|--------|-------|
| File size | 10,376 bytes |
| Line count | ~232 |
| Word count | ~1,850 |
| Token estimate | ~2,467 |

**Description:** Contains instructions for two distinct agent roles under one file. The first role (post-hoc analyzer) reads two skill files and two execution transcripts after a blind comparison to explain why the winner won and produce actionable `improvement_suggestions` with priority levels and categories. The second role (benchmark analyzer) reads in-progress `benchmark.json` data and produces freeform notes surfacing patterns hidden by aggregate statistics. Output schemas for both roles are included as JSON examples within the file.

---

### `agents/comparator.md`

| Metric | Value |
|--------|-------|
| File size | 7,287 bytes |
| Line count | ~166 |
| Word count | ~1,280 |
| Token estimate | ~1,707 |

**Description:** Blind A/B comparator agent. Receives two output paths, an eval prompt, and optional expectations. Generates a rubric with content and structure dimensions (each criterion scored 1-5), evaluates each output, determines a winner, and writes structured JSON to `comparison.json`. The rubric is dynamically generated per task type rather than fixed. Ties are explicitly discouraged. The file contains a complete output schema as an annotated JSON example.

---

### `agents/grader.md`

| Metric | Value |
|--------|-------|
| File size | 9,049 bytes |
| Line count | ~215 |
| Word count | ~1,720 |
| Token estimate | ~2,293 |

**Description:** Grader agent for evaluating predefined assertions against execution transcripts and output files. Introduces a two-job framing: grade outputs AND critique the evals themselves. Notable: the file instructs the grader to distinguish genuine pass from surface compliance (e.g., correct filename but wrong content). The grader also extracts implicit claims from outputs and verifies them beyond the predefined assertions. Includes `eval_feedback` output section for flagging weak or missing assertions. Full output schema with field descriptions is embedded.

---

### `references/schemas.md`

| Metric | Value |
|--------|-------|
| File size | 12,061 bytes |
| Line count | ~312 |
| Word count | ~1,790 |
| Token estimate | ~2,387 |

**Description:** Canonical JSON schema reference for all data files produced or consumed by the skill-creator workflow. Covers seven schemas: `evals.json`, `history.json`, `grading.json`, `metrics.json`, `timing.json`, `benchmark.json`, and `comparison.json` and `analysis.json`. Each schema entry includes a complete JSON example and a field-by-field description table. The `benchmark.json` section includes a warning that the viewer reads field names exactly and mismatches will produce empty values in the UI.

---

## 9. Structural Observations

### YAML Frontmatter

Present at lines 1-4. Contains two fields only: `name` and `description`. The description is 318 characters (single paragraph). No `compatibility`, `version`, `author`, or `tools` fields are present, consistent with the skill's own guidance that `compatibility` is "optional, rarely needed."

### Code Blocks

30 fenced code blocks (15 opening ` ``` ` markers). Languages used: `json` (majority), `bash`, `markdown` (for output format examples), and unlabeled blocks. Code blocks are used for:
- Shell command invocations (with flags and path placeholders)
- JSON schema examples
- Skill directory tree diagrams
- Output format templates
- `feedback.json` read example

### Lists vs. Prose

The file is approximately 55% prose and 45% structured content (code blocks + lists). Top-level sections use prose to explain rationale, then immediately follow with numbered step lists or code. Nested bullet lists appear in the skill writing guide and the iteration loop. The description optimization section is almost entirely prose with embedded code blocks for commands.

### Conditional Logic

Explicit environment branching is a distinctive structural feature. Three named environment variants appear:

1. **Default (Claude Code with subagents)** — the primary workflow
2. **Claude.ai-specific instructions** (lines 420-441) — subagents unavailable; sequential execution; skip quantitative benchmarking; skip description optimization; adapted packaging
3. **Cowork-specific instructions** (lines 445-456) — subagents available but no browser; use `--static` flag; different feedback download mechanism; all-caps emphasis on generating eval viewer before self-evaluation

### Templates

Two embedded templates are used in the workflow:

1. `eval_metadata.json` template (lines 190-197) — written per eval directory during runs
2. `assets/eval_review.html` — external HTML template for trigger eval query review; instructions specify the exact placeholder strings to replace (`__EVAL_DATA_PLACEHOLDER__`, `__SKILL_NAME_PLACEHOLDER__`, `__SKILL_DESCRIPTION_PLACEHOLDER__`)

### Examples

- Positive/negative query pair for description optimization (lines 350-356)
- Skill directory tree diagram showing domain organization pattern (lines 101-108)
- `evals.json` partial example (lines 147-159)
- `feedback.json` read example (lines 272-279)
- `timing.json` write example (lines 213-217)

### Constraints and Anti-patterns

The file includes several explicit prohibitions:
- "Do NOT use `/skill-test` or any other testing skill." (line 165)
- "don't spawn the with-skill runs first and then come back for baselines later" (line 171)
- "please use `generate_review.py` to create the viewer; there's no need to write custom HTML." (line 249)
- All-caps emphasis used once deliberately and self-consciously: "GENERATE THE EVAL VIEWER *BEFORE* evaluating inputs yourself." (line 451) — the surrounding text explicitly acknowledges the deviation from the skill's own style guidance ("I'm gonna go all caps here").

### Tone and Voice

The document uses first-person plural and direct address throughout. It contains casual register markers: "Cool? Cool." (line 30), "Good luck!" (line 485), parenthetical asides, and self-referential humor ("the rest of the skill :)"). This is consistent with the `Communicating with the user` section (lines 32-41), which explicitly models adaptive communication style and cautions against jargon. The skill performs its own advice about skill writing.

### Self-Reference

The skill contains a meta-layer: it teaches how to write skills and embeds an example of its own structural principles (progressive disclosure, anatomy diagram, writing patterns). The `Skill Writing Guide` subsection (lines 71-135) is a skill-writing reference embedded inside a skill. The 486-line length of the SKILL.md itself is within the `<500 lines ideal` constraint the file prescribes.
