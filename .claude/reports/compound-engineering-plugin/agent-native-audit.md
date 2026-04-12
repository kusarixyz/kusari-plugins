---
repository: EveryInc/compound-engineering-plugin
branch: main
skill-path: plugins/compound-engineering/skills/agent-native-audit
analyzed: 2026-04-11
---

# Skill Analysis: agent-native-audit


## 1. Overview

- **Skill name:** agent-native-audit
- **Title text:** "Agent-Native Architecture Audit" (35 characters)
- **Description (from frontmatter):** "Run comprehensive agent-native architecture review with scored principles" (72 characters)
- **Total files (recursive):** 1
- **Subdirectories:** 0
- **File list:**
  - `SKILL.md` (8237 bytes)

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Line count | 278 |
| Word count | 1274 |
| Character count | 8237 |
| Estimated token count (words / 0.75) | ~1699 |

---

## 3. Document Structure Depth

**Max heading depth:** H3 (level 3)

**Counts per level:**

| Level | Count |
|-------|-------|
| H1 | 1 |
| H2 | 13 |
| H3 | 39 |
| **Total** | **53** |

**All headings in order (with line numbers):**

| Line | Level | Text |
|------|-------|------|
| 8 | H1 | Agent-Native Architecture Audit |
| 12 | H2 | Core Principles to Audit |
| 23 | H2 | Workflow |
| 25 | H3 | Step 1: Load the Agent-Native Skill |
| 35 | H3 | Step 2: Launch Parallel Sub-Agents |
| 60 | H2 | Action Parity Audit |
| 61 | H3 | User Actions Found |
| 63 | H3 | Score: X/Y (percentage%) |
| 64 | H3 | Missing Agent Tools |
| 65 | H3 | Recommendations |
| 80 | H2 | Tools as Primitives Audit |
| 81 | H3 | Tool Analysis |
| 83 | H3 | Score: X/Y (percentage%) |
| 84 | H3 | Problematic Tools (workflows that should be primitives) |
| 85 | H3 | Recommendations |
| 104 | H2 | Context Injection Audit |
| 105 | H3 | Context Types Analysis |
| 107 | H3 | Score: X/Y (percentage%) |
| 108 | H3 | Missing Context |
| 109 | H3 | Recommendations |
| 122 | H2 | Shared Workspace Audit |
| 123 | H3 | Data Store Analysis |
| 125 | H3 | Score: X/Y (percentage%) |
| 126 | H3 | Isolated Data (anti-pattern) |
| 127 | H3 | Recommendations |
| 144 | H2 | CRUD Completeness Audit |
| 145 | H3 | Entity CRUD Analysis |
| 147 | H3 | Overall Score: X/Y entities with full CRUD (percentage%) |
| 148 | H3 | Incomplete Entities (list missing operations) |
| 149 | H3 | Recommendations |
| 167 | H2 | UI Integration Audit |
| 168 | H3 | Agent Action -> UI Update Analysis |
| 170 | H3 | Score: X/Y (percentage%) |
| 171 | H3 | Silent Actions (anti-pattern) |
| 172 | H3 | Recommendations |
| 191 | H2 | Capability Discovery Audit |
| 192 | H3 | Discovery Mechanism Analysis |
| 194 | H3 | Score: X/7 (percentage%) |
| 195 | H3 | Missing Discovery |
| 196 | H3 | Recommendations |
| 211 | H2 | Prompt-Native Features Audit |
| 212 | H3 | Feature Definition Analysis |
| 214 | H3 | Score: X/Y (percentage%) |
| 215 | H3 | Code-Defined Features (anti-pattern) |
| 216 | H3 | Recommendations |
| 221 | H3 | Step 3: Compile Summary Report |
| 226 | H2 | Agent-Native Architecture Review: [Project Name] |
| 228 | H3 | Overall Score Summary |
| 243 | H3 | Status Legend |
| 248 | H3 | Top 10 Recommendations by Impact |
| 253 | H3 | What's Working Excellently |
| 258 | H2 | Success Criteria |
| 266 | H2 | Optional: Single Principle Audit |

Note: H3 headings inside code blocks (lines 60-216) are embedded inside fenced backtick blocks as template output format strings. They are structurally part of the document source but serve as sub-agent output templates, not document navigation nodes. There are 5 such template sections (one per sub-agent group), each with 4 H3s, totaling ~20 H3s that are inside code fences. The remaining H3s are top-level document headings.

---

## 4. Content Specificity Assessment

**Score: 3 / 5**

The skill is structurally detailed but operationally generic. It defines eight audit dimensions and supplies concrete output templates (table schemas, score formats, section headers) for each sub-agent. However, it does not reference any specific files, APIs, or patterns from a target codebase -- all enumeration is delegated to the sub-agents at runtime. The instructions are moderately specific about what to search for but leave the actual search strategy open.

**Justification excerpts:**

1. Specific (positive): Each sub-agent block specifies exact search strategies and output table schemas.
   > "Search for API service files, fetch calls, form handlers" / "| Action | Location | Agent Tool | Status |"
   The output format is locked -- numeric scores must be "X out of Y (percentage%)" format.

2. Generic (negative): No codebase-specific file paths, no tool names, no framework assumptions are hardcoded.
   > "Find and read ALL agent tool files" -- no guidance on where these live, what naming convention to expect, or what framework they target.

3. Partially specific: The seven capability discovery mechanisms are enumerated concretely (onboarding flow, slash commands, empty state guidance, etc.), giving the sub-agent a fixed checklist rather than open-ended exploration. Score is fixed at X/7.

---

## 5. Internal File References

None. The SKILL.md contains no markdown links (`[text](path)`) and no inline file path references pointing to files within the skill or repository.

---

## 6. Skill Cross-References

One reference to another skill in the same plugin:

| Line | Reference | Type |
|------|-----------|------|
| 30 | `/compound-engineering:agent-native-architecture` | Slash command invocation (Step 1 instructs loading this skill first via the command) |

The referenced skill (`agent-native-architecture`) is a separate skill in the same compound-engineering plugin. It is invoked with option 7 (action parity) to load full reference material before the audit sub-agents run.

---

## 7. Agent References

The skill is built around sub-agent orchestration. References:

| Line | Reference | Type |
|------|-----------|------|
| 37 | `Task tool with subagent_type: Explore` | Sub-agent launch mechanism |
| 44 | `<sub-agents>` block | Custom XML tag delimiting 8 parallel sub-agent prompt templates |
| 219 | `</sub-agents>` | Close of sub-agent block |
| 260 | "All 8 sub-agents complete their audits" | Success criterion |
| 268 | "only run that sub-agent" | Conditional single-principle mode |

The skill does not reference any named agent files (`.md` agent definitions). Sub-agents are launched inline via prompt templates embedded in the skill body, not via named agent references.

---

## 8. Other Markdown File Analysis

None. The skill directory contains only `SKILL.md`. There are no other markdown files.

---

## 9. Structural Observations

**YAML Frontmatter**

Present. Fields:
```yaml
name: agent-native-audit
description: Run comprehensive agent-native architecture review with scored principles
argument-hint: "[optional: specific principle to audit]"
disable-model-invocation: true
```

`disable-model-invocation: true` is notable -- the skill suppresses direct model calls and relies entirely on sub-agent dispatch via the Task tool. The skill itself acts as an orchestration manifest, not an interactive prompt.

**Code blocks**

Multiple fenced code blocks (backtick-delimited). Identified uses:
- One block containing the slash command invocation (`/compound-engineering:agent-native-architecture`) -- line ~29-31
- Eight blocks containing sub-agent prompt templates, one per principle -- the largest section of the document (~lines 47-218)
- One block containing the final summary report template in markdown -- lines ~224-256

Approximately 10 code fences total. The majority of the document body (roughly 170 of 278 lines) is inside code blocks.

**Lists vs prose**

- 51 list items (bullet and numbered) outside code blocks
- Prose paragraphs: minimal -- the intro paragraph (lines 9-10) and brief transition sentences between steps are the only prose. The document is predominantly structured lists and code blocks.
- 20 table rows across 8 tables (one per sub-agent output template, all inside code blocks)

**Conditional logic**

One conditional branch: the "Optional: Single Principle Audit" section (line 266) activates when `$ARGUMENTS` specifies a single principle. Valid argument forms are enumerated: named strings (`action parity`, `tools`, `context`, etc.) and numeric aliases (`1` through `8`). This is the only branching point in the skill.

**Templates**

The document is primarily a template document. Each of the 8 sub-agent blocks is a self-contained prompt template with:
- A task description using imperative verbs
- A numbered task list specifying what to enumerate and assess
- A fixed output format section specifying exact H2/H3 headers and table schemas the sub-agent must produce

The Step 3 section provides a final report assembly template with a pre-defined markdown table structure (8-row score summary, status legend, top 10 recommendations table, strengths section).

**Examples**

No worked examples with actual codebase data. All examples are structural templates with placeholder values (`X/Y`, `[Project Name]`, `[List top 5 strengths]`). The argument hint examples are concrete string values (`"action parity"`, `1` through `8`).

**Constraints**

- Scoring format is constrained: must be `X/Y (percentage%)` format
- Capability Discovery score is fixed-denominator: must be `X/7`
- Success criteria (lines 258-262) enumerate 5 explicit completion conditions using a checkbox list
- Sub-agent output structure is constrained by the template headers inside each code block
