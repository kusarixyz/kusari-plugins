---
repository: EveryInc/compound-engineering-plugin
branch: main
skill-path: plugins/compound-engineering/skills/ce-compound
analyzed: 2026-04-11
---

# Skill Analysis: ce-compound


## 1. Overview

**Skill name:** `ce:compound`

**Title text:** `/compound`
**Title char length:** 9

**Description:** `Document a recently solved problem to compound your team's knowledge`
**Description char length:** 67

**Total files (recursive):** 4
- `SKILL.md`
- `assets/resolution-template.md`
- `references/schema.yaml`
- `references/yaml-schema.md`

**Subdirectories:** 2
- `assets/`
- `references/`

**File list with sizes:**

| File | Bytes |
|------|-------|
| `SKILL.md` | 31139 |
| `assets/resolution-template.md` | 1996 |
| `references/schema.yaml` | 6980 |
| `references/yaml-schema.md` | 4511 |

**Total skill size:** 44626 bytes

---

## 2. SKILL.md Metrics

**Known file size:** 31139 bytes

**Measured via WebFetch analysis** (model-counted; injected prompt text inflates raw model counts — figures below are best estimates from content analysis):

| Metric | Value | Note |
|--------|-------|------|
| Line count | ~700 | Model-reported 823 includes injected prompt lines |
| Word count | ~5800–6200 | Model-reported 6847 includes injected prompt words |
| Estimated token count | ~7700–8300 | word count / 0.75 |
| Character count | ~31000 | Byte size (31139) is the most reliable anchor; file is ASCII-dominant |

**Authoritative anchor:** The GitHub API reports `SKILL.md` at exactly **31139 bytes**. Character count for a UTF-8 ASCII-dominant file is approximately equal to byte count: **~31139 characters**.

Derived estimates:
- Average English prose: ~5 chars/word → ~6228 words
- At 0.75 words/token → **~8304 tokens**
- At ~45 chars/line → **~692 lines**

---

## 3. Document Structure Depth

**YAML frontmatter:** Present (lines 1–4, between `---` delimiters)

```yaml
name: ce:compound
description: Document a recently solved problem to compound your team's knowledge
```

**All headings in order:**

| # | Level | Heading Text |
|---|-------|-------------|
| 1 | H1 | `/compound` |
| 2 | H2 | `Purpose` |
| 3 | H2 | `Usage` |
| 4 | H2 | `Support Files` |
| 5 | H2 | `Execution Strategy` |
| 6 | H3 | `Full Mode` |
| 7 | H3 | `Phase 0.5: Auto Memory Scan` |
| 8 | H3 | `Phase 1: Research` |
| 9 | H4 | `1. **Context Analyzer**` |
| 10 | H4 | `2. **Solution Extractor**` |
| 11 | H4 | `3. **Related Docs Finder**` |
| 12 | H4 | `4. **Session Historian** (foreground, after launching the above — only if the user opted in)` |
| 13 | H3 | `Phase 2: Assembly & Write` |
| 14 | H3 | `Phase 2.5: Selective Refresh Check` |
| 15 | H3 | `Discoverability Check` |
| 16 | H3 | `Phase 3: Optional Enhancement` |
| 17 | H3 | `Lightweight Mode` |
| 18 | H2 | `What It Captures` |
| 19 | H2 | `Preconditions` |
| 20 | H2 | `What It Creates` |
| 21 | H2 | `Common Mistakes to Avoid` |
| 22 | H2 | `Success Output` |
| 23 | H2 | `The Compounding Philosophy` |
| 24 | H2 | `Auto-Invoke` |
| 25 | H2 | `Output` |
| 26 | H2 | `Applicable Specialized Agents` |
| 27 | H3 | `Code Quality & Review` |
| 28 | H3 | `Specific Domain Experts` |
| 29 | H3 | `Enhancement & Research` |
| 30 | H3 | `When to Invoke` |
| 31 | H2 | `Related Commands` |

**Total headings:** 31

**Count by level:**
- H1: 1
- H2: 15
- H3: 10
- H4: 4

**Maximum depth:** H4 (4 levels)

**Structural note:** The H4 headings are used exclusively inside `Phase 1: Research` to enumerate the four parallel subagent roles. No other section uses H4. The `Execution Strategy` → `Full Mode` → `Phase 1: Research` → agent roles pattern is the deepest nesting in the document.

---

## 4. Content Specificity Assessment

**Rating: 5 / 5**

This is maximally specific operational documentation. Every section prescribes exact behavior with no ambiguity left to interpretation.

**Justification excerpts:**

1. Platform-specific tool names with fallback chains:
   > "Present the user with two options before proceeding, using the platform's blocking question tool (`AskUserQuestion` in Claude Code, `request_user_input` in Codex, `ask_user` in Gemini). If no question tool is available, present the options and wait for the user's reply."

2. Overlap assessment with a precise decision matrix (not vague guidance — a literal table mapping overlap level to exact action: update vs. create new doc).

3. Discoverability Check includes calibration examples with explicit tone instructions: "Keep the tone informational, not imperative. Express timing as description, not instruction — 'relevant when implementing or debugging in documented areas' rather than 'check before implementing or debugging.'"

4. Subagent dispatch specifies model tier: "Dispatch on the mid-tier model (e.g., `model: 'sonnet'` in Claude Code) — the synthesis feeds into compound assembly and doesn't need frontier reasoning."

5. Related Docs Finder includes a grep-first filtering algorithm with explicit thresholds (>25 candidates → tighten; <3 candidates → broaden) and instructions to read only the first 30 lines of candidates before full reads.

The document also includes a `<critical_requirement>` block, a `<preconditions>` XML block with enforcement mode, XML `<parallel_tasks>` and `<sequential_tasks>` delimiters, and an `<auto_invoke>` block with trigger phrases — all highly specific structural markers.

---

## 5. Internal File References

Every file reference found in SKILL.md:

| Reference | Type | Exists in skill | Context |
|-----------|------|-----------------|---------|
| `references/schema.yaml` | Relative path | Yes | Read by Context Analyzer and Solution Extractor for enum validation and track classification |
| `references/yaml-schema.md` | Relative path | Yes | Read by Context Analyzer for category-to-directory mapping |
| `assets/resolution-template.md` | Relative path | Yes | Read by orchestrator during Phase 2 assembly for section structure |
| `docs/solutions/` | Project-relative path | No (target output dir) | Output destination for all created documentation |
| `docs/solutions/<category>/` | Project-relative path | No (target output dir) | Categorized subdirectory for output docs |
| `docs/solutions/[category]/[filename].md` | Project-relative path | No (output artifact) | Final written file |
| `docs/solutions/performance-issues/n-plus-one-brief-generation.md` | Project-relative path | No (example) | Used in Success Output example |
| `docs/solutions/performance-issues/n-plus-one-queries.md` | Project-relative path | No (example) | Used in alternate success output example |
| `AGENTS.md` | Project-relative path | No | Discoverability Check target — project instruction file |
| `CLAUDE.md` | Project-relative path | No | Discoverability Check target — project instruction file |
| `MEMORY.md` | Harness-path | No | Auto memory scan source; read from auto memory directory |
| `~/.claude/projects/` | Absolute path | No | Session Historian search path for Claude Code sessions |
| `~/.codex/sessions/` | Absolute path | No | Session Historian search path for Codex sessions |
| `~/.cursor/projects/` | Absolute path | No | Session Historian search path for Cursor sessions |
| `docs/solutions/patterns/` | Project-relative path | No (example) | Referenced in refresh scope examples |

**Summary:** 3 internal skill files referenced (all exist), 12 external/output paths referenced (none exist within the skill boundary).

---

## 6. Skill Cross-References

| Referenced Skill | Context | Location in SKILL.md |
|-----------------|---------|----------------------|
| `ce:compound` | Self-reference (invocation syntax) | Usage section, Auto-Invoke section |
| `ce:compound-refresh` | Follow-up skill for refreshing stale docs; invoked selectively after Phase 2.5 | Phase 2.5: Selective Refresh Check (multiple references); Lightweight Mode output block |
| `ce:plan` | Listed as related command: "Planning workflow (references documented solutions)" | Related Commands section |

**Referenced via `/` command syntax:**
- `/ce:compound [context]`
- `/ce:compound-refresh [scope]`
- `/ce:plan`
- `/research [topic]` (non-namespaced; may be a different plugin or built-in)

---

## 7. Agent References

All agent identifiers use the `compound-engineering:<namespace>:<agent-name>` pattern.

**Research namespace:**

| Agent | Dispatch method | Context |
|-------|----------------|---------|
| `compound-engineering:research:session-historian` | Foreground subagent | Phase 1; reads session files outside working directory; dispatched after background agents; mid-tier model specified |
| `compound-engineering:research:best-practices-researcher` | Optional post-documentation | Applicable Specialized Agents section |
| `compound-engineering:research:framework-docs-researcher` | Optional post-documentation | Applicable Specialized Agents section |

**Review namespace:**

| Agent | Trigger condition | Context |
|-------|------------------|---------|
| `compound-engineering:review:performance-oracle` | Auto-triggered for `performance_issue` | Phase 3: Optional Enhancement |
| `compound-engineering:review:security-sentinel` | Auto-triggered for `security_issue` | Phase 3: Optional Enhancement |
| `compound-engineering:review:data-integrity-guardian` | Auto-triggered for `database_issue` | Phase 3: Optional Enhancement |
| `compound-engineering:review:code-simplicity-reviewer` | Auto-triggered for any code-heavy issue | Phase 3: Optional Enhancement |
| `compound-engineering:review:kieran-rails-reviewer` | Auto-triggered for Ruby/Rails repos | Phase 3: Optional Enhancement |
| `compound-engineering:review:kieran-python-reviewer` | Auto-triggered for Python repos | Phase 3: Optional Enhancement |
| `compound-engineering:review:kieran-typescript-reviewer` | Auto-triggered for TypeScript/JS repos | Phase 3: Optional Enhancement |
| `compound-engineering:review:pattern-recognition-specialist` | Optional post-documentation | Applicable Specialized Agents section |

**Total agents referenced:** 11 (3 research, 8 review)

**Note:** Phase 3 agents are marked optional and auto-triggered conditionally on `problem_type`. The Session Historian is the only agent dispatched within the primary execution path (Phase 1), and only when the user opts in to session history search.

---

## 8. Other Markdown File Analysis

### `assets/resolution-template.md`

**Size:** 1996 bytes
**Lines:** 97
**Words:** 331
**Characters:** ~2447 (model-reported 2447; consistent with byte size of 1996 given markdown formatting)

**Purpose:** Provides two track-specific templates — Bug Track and Knowledge Track — for the body structure of output documentation files. Each template includes YAML frontmatter placeholder fields and section headers matching the track's documentation pattern.

**Structure:**
- H1: `Resolution Templates`
- H2: `Bug Track Template` (with fenced markdown code block containing full template)
- H2: `Knowledge Track Template` (with fenced markdown code block containing full template)

**Bug Track Template sections:** Problem, Symptoms, What Didn't Work, Solution, Why This Works, Prevention, Related Issues

**Knowledge Track Template sections:** Context, Guidance, Why This Matters, When to Apply, Examples, Related

**No YAML frontmatter** on the file itself. No cross-references to other files.

---

### `references/yaml-schema.md`

**Size:** 4511 bytes
**Lines:** 115 (model-reported)
**Words:** 652 (model-reported)
**Characters:** ~4511 (consistent with byte size)

**Purpose:** Human-readable companion to `schema.yaml`. Documents the track system (bug vs. knowledge), required fields per track, optional fields, backward compatibility rules, category-to-directory mapping, and validation rules.

**Structure:**
- H1: `YAML Frontmatter Schema`
- H2: `Tracks` (table: Track | problem_types | Description)
- H2: `Required Fields (both tracks)`
- H2: `Bug Track Fields`
- H2: `Knowledge Track Fields`
- H2: `Optional Fields (both tracks)`
- H2: `Optional Fields (bug track only)`
- H2: `Backward Compatibility`
- H2: `Category Mapping` (13 mappings listed)
- H2: `Validation Rules` (9 rules)

**No YAML frontmatter.** No cross-references beyond intra-skill mention of `schema.yaml` in the title.

---

### `references/schema.yaml`

**Size:** 6980 bytes
**Lines:** 148 (model-reported)
**Words:** 547 (model-reported)
**Characters:** ~6980

**Purpose:** Canonical YAML schema defining all frontmatter fields, enum values, and validation constraints for output documentation files. This is the machine-readable contract that subagents read directly.

**Not a markdown file** — included here as the only non-markdown reference file.

**Key schema contents (from yaml-schema.md description):**
- Track classification: bug track vs. knowledge track based on `problem_type`
- 13 `problem_type` enum values across both tracks
- 15 `component` enum values
- 4 `severity` levels
- Required/optional field rules per track
- `root_cause` enum (17 values), `resolution_type` enum (10 values)
- `tags` format: lowercase hyphen-separated
- `date` format: `YYYY-MM-DD`
- `rails_version` format: `X.Y.Z`

---

## 9. Structural Observations

### YAML Frontmatter
SKILL.md has a frontmatter block at lines 1–4 with `name` and `description` only. No `version`, `author`, `tags`, or other fields. This is a minimal frontmatter consistent with skill registration requirements.

### XML Structural Markers
The file uses custom XML tags as execution-phase delimiters — a pattern not common in standard markdown:
- `<critical_requirement>` — enforces the single-file-output rule and subagent data-only return constraint (appears twice: once in Full Mode, once in Lightweight Mode)
- `<parallel_tasks>` / `</parallel_tasks>` — wraps Phase 1 subagent specs and Phase 3 optional agents
- `<sequential_tasks>` / `</sequential_tasks>` — wraps Phase 2 assembly steps
- `<preconditions enforcement="advisory">` with child `<check>` elements — advisory gate before execution
- `<auto_invoke>` with `<trigger_phrases>` and `<manual_override>` children — defines automatic invocation conditions

### Code Blocks
Approximately 14 fenced code blocks identified:
- 1 with `bash` language tag (Usage section showing invocation syntax)
- Remainder are plain/untagged, used for: user-facing option prompts, session historian output format spec, grep pattern examples, discoverability addition examples, success output templates (two variants), compounding philosophy feedback loop diagram, lightweight output template

### Lists vs. Prose
The document is predominantly prose with embedded lists. Bullet lists are used heavily within subagent task specs (responsibilities, output fields, search strategy steps). The Related Docs Finder section contains the most list-dense content, with a 7-step grep-first filtering algorithm. Two tables appear: the overlap assessment decision matrix (Phase 2) and the Common Mistakes to Avoid table.

### Decision Tables
One explicit decision table in Phase 2 maps overlap level (High/Moderate/Low) to action (update existing / create new with flag / create new). One table in Common Mistakes to Avoid maps wrong behaviors to correct ones.

### Conditional Logic
The document encodes branching logic explicitly:
- Full mode vs. Lightweight mode (user-selected at start)
- Session Historian dispatch conditional on user opt-in
- Phase 3 agent selection conditional on `problem_type`
- Stack-specific kieran reviewer selection (Ruby/Rails / Python / TypeScript / other)
- Discoverability Check edit conditional on whether instruction file already surfaces knowledge store
- Phase 2.5 refresh decision based on five-dimensional overlap criteria

### Templates
Two output templates are defined verbatim in the file:
1. Success output block (full mode, new doc created)
2. Alternate success output block (full mode, existing doc updated)
3. Lightweight mode output block

These templates include placeholder tokens like `[category]`, `[filename]`, and example values for illustration.

### Examples
Named concrete examples appear throughout:
- `docs/solutions/performance-issues/n-plus-one-brief-generation.md` — referenced in success output template
- `docs/solutions/performance-issues/n-plus-one-queries.md` — referenced in alternate success output
- `/ce:compound-refresh plugin-versioning-requirements` — refresh scope example
- `/ce:compound-refresh payments` — refresh scope example
- `/ce:compound-refresh performance-issues` — refresh scope example
- `/ce:compound-refresh critical-patterns` — refresh scope example
- Discoverability addition examples: directory listing line vs. headed section

### Constraints (explicit enforcement statements)
- "Do NOT pre-select a mode. Do NOT skip this prompt."
- "Subagents return TEXT DATA to the orchestrator. They must NOT use Write, Edit, or create any files."
- "WAIT for all Phase 1 subagents to complete before proceeding." (Phase 2)
- "WAIT for Phase 2 to complete before proceeding." (Phase 3)
- "Always capture the new learning first. Refresh is a targeted maintenance follow-up, not a prerequisite."
- "Do not invoke `ce:compound-refresh` without an argument unless the user explicitly wants a broad sweep."
- Lightweight mode: "No subagents are launched. No parallel tasks. One file written."

### Progressive Disclosure Pattern
The Support Files section explicitly instructs: "Read them on-demand at the step that needs them — do not bulk-load at skill start." This is a deliberate token-conservation design decision, directing agents to lazy-load the three support files only when they are needed by each phase rather than preloading all at the start of execution.
