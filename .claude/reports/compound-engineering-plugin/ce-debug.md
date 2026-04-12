---
skill: ce-debug
repo: EveryInc/compound-engineering-plugin
branch: main
path: plugins/compound-engineering/skills/ce-debug
analyzed: 2026-04-11
---

# Skill Analysis: ce-debug

## 1. Overview

**Skill name:** ce-debug
**Title text:** `Debug and Fix` (13 characters)
**Description (from frontmatter):** `Systematically find root causes and fix bugs. Use when debugging errors, investigating test failures, reproducing bugs from issue trackers (GitHub, Linear, Jira), or when stuck on a problem after failed fix attempts. Also use when the user says 'debug this', 'why is this failing', 'fix this bug', 'trace this error', or pastes stack traces, error messages, or issue references.`
**Description character count:** 382

**Total files (recursive):** 3
**Subdirectories:** 1 (`references/`)

**File list:**
| File | Bytes |
|------|-------|
| `SKILL.md` | 12215 |
| `references/anti-patterns.md` | 6213 |
| `references/investigation-techniques.md` | 6152 |

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Line count | 191 |
| Word count | 1939 |
| Estimated token count (words / 0.75) | 2585 |
| Character count | 12215 |

---

## 3. Document Structure Depth

**Max depth:** H4 (4 levels)
**Heading counts by level:** H1: 2, H2: 3, H3: 5, H4: 3

Note: The second H1 (`## Debug Summary` at line 177) is inside a fenced code block and is rendered as literal text, not a document heading. As a structural heading, the document has H1: 1, H2: 3, H3: 5, H4: 3.

| Line | Level | Text |
|------|-------|------|
| 7 | H1 | `Debug and Fix` |
| 13 | H2 | `Core Principles` |
| 22 | H2 | `Execution Flow` |
| 36 | H3 | `Phase 0: Triage` |
| 57 | H3 | `Phase 1: Investigate` |
| 59 | H4 | `1.1 Reproduce the bug` |
| 68 | H4 | `1.2 Trace the code path` |
| 89 | H3 | `Phase 2: Root Cause` |
| 108 | H2 | `Debug Summary` (inside code block -- literal, not structural) |
| 108 | H3 (structural) | `Present findings` |
| 132 | H3 | `Smart escalation` |
| 147 | H3 | `Phase 3: Fix` |
| 172 | H3 | `Phase 4: Close` |
| 177 | H4 (in code block) | `Debug Summary` (code block content, structural H4 wrapper) |

**Corrected structural heading list (document headings only):**

| Line | Level | Text |
|------|-------|------|
| 7 | H1 | `Debug and Fix` |
| 13 | H2 | `Core Principles` |
| 22 | H2 | `Execution Flow` |
| 36 | H3 | `Phase 0: Triage` |
| 57 | H3 | `Phase 1: Investigate` |
| 59 | H4 | `1.1 Reproduce the bug` |
| 68 | H4 | `1.2 Trace the code path` |
| 89 | H3 | `Phase 2: Root Cause` |
| 108 | H3 | `Present findings` |
| 132 | H3 | `Smart escalation` |
| 147 | H3 | `Phase 3: Fix` |
| 172 | H3 | `Phase 4: Close` |

**Per-level counts (structural headings only):**
- H1: 1
- H2: 2 (Core Principles, Execution Flow)
- H3: 7 (Phase 0-4, Present findings, Smart escalation)
- H4: 2 (1.1, 1.2)

---

## 4. Content Specificity Assessment

**Score: 5/5**

The skill is operationally prescriptive throughout. It does not describe what debugging is -- it specifies exactly how the agent must behave at each step.

**Excerpt 1 -- precise trigger conditions for questions (Phase 0):**
> "Do not ask questions by default -- investigate first (read code, run tests, trace errors). Only ask when a genuine ambiguity blocks investigation and cannot be resolved by reading code or running tests. When asking, ask one specific question."

This defines the exact condition set for a class of agent behavior rather than giving a vague directive.

**Excerpt 2 -- concrete escalation table with named patterns (Phase 2 Smart escalation):**

The table maps four specific observable patterns (hypotheses pointing to different subsystems; self-contradicting evidence; local vs CI failure; fix works but prediction wrong) to named diagnoses and prescribed next moves. No ambiguity about which row applies.

**Excerpt 3 -- named platform tool variants (Phase 2 Present findings):**
> "use the platform's question tool -- `AskUserQuestion` in Claude Code, `request_user_input` in Codex, `ask_user` in Gemini"

Specifies exact API symbols per platform rather than deferring to the reader.

**Excerpt 4 -- conditional triggers for post-fix behaviors (Phase 3):**
> "Conditional defense-in-depth (trigger: grep for the root-cause pattern found it in other files)"
> "Conditional post-mortem (trigger: the bug was in production, OR the pattern appears in 3+ locations)"

Named conditions gate optional behaviors with specific thresholds (3+ locations).

---

## 5. Internal File References

| Reference | Line(s) | Context |
|-----------|---------|---------|
| `references/investigation-techniques.md` | 65, 79 | Load when bug does not reproduce after 2-3 attempts; use `git bisect` guidance |
| `references/anti-patterns.md` | 93 | Read before forming hypotheses in Phase 2 |

Both references are conditional -- they are pulled in at specific decision points during execution, not loaded upfront.

---

## 6. Skill Cross-References

| Reference | Line(s) | Context |
|-----------|---------|---------|
| `/proof` | 119, 190 | Offer after Phase 2 root cause presentation and in Phase 4 handoff options |
| `/ce:brainstorm` | 120, 138, 188 (indirect) | Suggest when root cause reveals a design problem; also in smart escalation table |
| `/ce:compound` | 168, 188 | Suggest when systemic gap pattern found in 3+ files; Phase 4 handoff option |

All three are offered as user-choice options at explicit handoff points, not invoked autonomously.

---

## 7. Agent References

| Reference | Line | Context |
|-----------|------|---------|
| `agent-browser` | 63 | Preferred tool for browser bug reproduction in Phase 1 |

`agent-browser` is referenced as optional (`if installed`), with a fallback chain: MCP browser tools, direct URL testing, screenshot capture.

---

## 8. Other Markdown File Analysis

### references/anti-patterns.md

| Metric | Value |
|--------|-------|
| File size | 6213 bytes |
| Line count | 91 |
| Word count | 987 |
| Estimated token count (words / 0.75) | 1316 |

**Headings:**

| Line | Level | Text |
|------|-------|------|
| 1 | H1 | `Debugging Anti-Patterns` |
| 7 | H2 | `Prediction Quality` |
| 27 | H2 | `Shotgun Debugging` |
| 39 | H2 | `Confirmation Bias` |
| 52 | H2 | `"It Works Now, Move On"` |
| 65 | H2 | `Thoughts That Signal You Are About to Shortcut` |
| 81 | H2 | `Smart Escalation Patterns` |

Max depth: H2. H1: 1, H2: 6.

Structure: flat, each section is a named anti-pattern with a `How it feels/looks` and `The defense/fix` pattern. Heavy use of bold labels for sub-structure within H2 sections. No code blocks.

---

### references/investigation-techniques.md

| Metric | Value |
|--------|-------|
| File size | 6152 bytes |
| Line count | 161 |
| Word count | 890 |
| Estimated token count (words / 0.75) | 1187 |

**Structural headings (excluding comment lines inside code blocks):**

| Line | Level | Text |
|------|-------|------|
| 1 | H1 | `Investigation Techniques` |
| 7 | H2 | `Root-Cause Tracing` |
| 41 | H2 | `Git Bisect for Regressions` |
| 65 | H2 | `Intermittent Bug Techniques` |
| 92 | H2 | `Framework-Specific Debugging` |
| 94 | H3 | `Rails` |
| 100 | H3 | `Node.js` |
| 106 | H3 | `Python` |
| 114 | H2 | `Race Condition Investigation` |
| 137 | H2 | `Browser Debugging` |

Note: lines 49-50, 142, 145, 148, 153 contain `#` characters inside fenced bash code blocks (comments) -- not document headings.

Max depth: H3. H1: 1, H2: 6, H3: 3.

Contains 7 fenced code blocks: root-cause instrumentation snippet, git bisect commands, automated bisect command, statistical reproduction loop, browser debugging command sequence (multiple blocks), and individual framework technique snippets.

---

## 9. Structural Observations

### YAML Frontmatter
Three keys present in SKILL.md:
- `name: ce-debug`
- `description:` (382 chars, multi-trigger, includes verbatim user phrases for matching)
- `argument-hint: "[issue reference, error message, test path, or description of broken behavior]"`

The description is unusually long and explicitly lists platform-specific issue tracker formats (GitHub `#123`, `org/repo#123`, Linear, Jira) and verbatim user phrases. This is intentional for trigger matching.

### Code Blocks
SKILL.md contains 1 fenced code block (lines 176-186): the `## Debug Summary` structured output template in Phase 4. It is a fill-in-the-blanks template, not executable code.

`references/anti-patterns.md`: 0 code blocks.
`references/investigation-techniques.md`: 7 code blocks -- all executable (bash commands, language-specific debug snippets).

### Lists vs Prose
SKILL.md is primarily prose-driven with numbered lists for principles and lettered/bulleted lists for decision branches. Phase flow uses a markdown table for structure. Smart escalation uses a 3-column decision table. The mix is intentional: tables for decision routing, prose for nuanced conditions.

`anti-patterns.md` is entirely prose with bold labels as inline structure.
`investigation-techniques.md` mixes prose with code blocks, using bulleted lists for technique options.

### Conditional Logic
Explicit conditional triggers appear 6 times in SKILL.md:
1. Issue tracker reference detection -- branch in Phase 0 (GitHub vs other trackers vs direct input)
2. Browser bug detection -- branch in Phase 1.1 (`agent-browser` if installed, else fallback chain)
3. Non-reproduction after 2-3 attempts -- load `references/investigation-techniques.md`
4. Regression signal ("it worked before") -- use `git bisect`
5. Defense-in-depth -- triggered if root-cause pattern found in other files via grep
6. Post-mortem -- triggered if production bug OR pattern in 3+ locations

### Templates
One output template: the Phase 4 `## Debug Summary` code block with 6 named fields (Problem, Root Cause, Recommended Tests, Fix, Prevention, Confidence). The template is instructed to be produced as the structured close of every debugging session.

### Examples
`anti-patterns.md` contains two structured bad/good examples for prediction quality (annotated as `Bad prediction` and `Good prediction`). `investigation-techniques.md` contains one worked example (API 500 error traced backward through UserController to UserRepo). SKILL.md itself contains no inline examples -- examples are delegated to reference files.

### Constraints (explicit "do not" rules)
- Do not propose a fix until the full causal chain is explained (stated twice -- Phase 2 header and reminder)
- Do not ask questions by default
- Do not change multiple things at once
- Do not skip the causal chain gate without explicit user authorization
- Do not suggest brainstorm for bugs that are large but have a clear fix
- Do not overwrite uncommitted user changes without confirmation
- If fix attempt #3 fails, do not try a fourth -- diagnose first

### Escalation Architecture
The skill has a named smart escalation procedure used in two places: Phase 2 (after 2-3 failed hypotheses) and Phase 3 (after 3 failed fix attempts). Both reference the same 4-row decision table mapping observable patterns to diagnoses and next moves. The escalation is symmetrical across investigation and fixing.

### Intra-document Reminder Pattern
Core principles are explicitly re-stated at the top of Phase 2 (`Reminder: investigate before fixing...`) and Phase 3 (`Reminder: one change at a time...`). The SKILL.md itself calls this out in the Core Principles section: "They are repeated at decision points because they matter most when the pressure to skip them is highest." This is a deliberate design choice to combat LLM drift toward shortcutting under pressure.
