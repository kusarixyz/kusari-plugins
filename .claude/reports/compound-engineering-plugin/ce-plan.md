---
repository: EveryInc/compound-engineering-plugin
branch: main
skill-path: plugins/compound-engineering/skills/ce-plan
analyzed: 2026-04-11
---

# Skill Analysis: ce:plan

## 1. Overview

**Skill name:** ce:plan
**Title text (H1):** `Create Technical Plan`
**Title char length:** 21 characters

**Description text (from YAML frontmatter):**
> Create structured plans for any multi-step task -- software features, research workflows, events, study plans, or any goal that benefits from structured breakdown. Also deepen existing plans with interactive review of sub-agent findings. Use for plan creation when the user says 'plan this', 'create a plan', 'write a tech plan', 'plan the implementation', 'how should we build', 'what's the approach for', 'break this down', 'plan a trip', 'create a study plan', or when a brainstorm/requirements document is ready for planning. Use for plan deepening when the user says 'deepen the plan', 'deepen my plan', 'deepening pass', or uses 'deepen' in reference to a plan. For exploratory or ambiguous requests where the user is unsure what to do, prefer ce:brainstorm first.

**Description char length:** 698 characters

**Total files (recursive):** 5
**Subdirectories:** 1 (`references/`)

**File list:**
| File | Type | Size (bytes) |
|---|---|---|
| `SKILL.md` | blob | 43,594 |
| `references/deepening-workflow.md` | blob | 15,349 |
| `references/plan-handoff.md` | blob | 5,223 |
| `references/universal-planning.md` | blob | 8,553 |
| `references/visual-communication.md` | blob | 3,293 |

**Total content size:** 76,012 bytes across all files.

---

## 2. SKILL.md Metrics

| Metric | Value |
|---|---|
| Line count | 730 |
| Word count | 6,293 |
| Estimated token count (words / 0.75) | ~8,391 |
| Character count | 43,594 |

---

## 3. Document Structure Depth

**Maximum heading depth:** 5 (H5)

**Count per level:**
| Level | Count |
|---|---|
| H1 (`#`) | 2 (line 7: workflow title; line 452: embedded plan template title) |
| H2 (`##`) | 26 |
| H3 (`###`) | 14 |
| H4 (`####`) | 29 |
| H5 (`#####`) | 4 |
| **Total** | **75** |

**Note:** H1 at line 452 is inside a fenced code block (the core plan template). The effective document H1 is line 7 only. The structural depth of the live document (outside code blocks) is H4. H5 appears only in the confidence-check subsections (5.3.x).

**All headings in order with line numbers:**

| Line | Level | Text |
|---|---|---|
| 7 | H1 | Create Technical Plan |
| 15 | H2 | Interaction Method |
| 21 | H2 | Feature Description |
| 31 | H2 | Core Principles |
| 41 | H2 | Plan Quality Bar |
| 55 | H2 | Workflow |
| 57 | H3 | Phase 0: Resume, Source, and Scope |
| 59 | H4 | 0.1 Resume Existing Plan Work When Appropriate |
| 78 | H4 | 0.1b Classify Task Domain |
| 88 | H4 | 0.2 Find Upstream Requirements Document |
| 99 | H4 | 0.3 Use the Source Document as Primary Input |
| 117 | H4 | 0.4 No-Requirements-Doc Fallback |
| 137 | H4 | 0.5 Classify Outstanding Questions Before Planning |
| 151 | H4 | 0.6 Assess Plan Depth |
| 161 | H3 | Phase 1: Gather Context |
| 163 | H4 | 1.1 Local Research (Always Runs) |
| 186 | H4 | 1.1b Detect Execution Posture Signals |
| 199 | H4 | 1.2 Decide on External Research |
| 236 | H4 | 1.3 External Research (Conditional) |
| 243 | H4 | 1.4 Consolidate Research |
| 253 | H4 | 1.4b Reclassify Depth When Research Reveals External Contract Surfaces |
| 265 | H4 | 1.5 Flow and Edge-Case Analysis (Conditional) |
| 276 | H3 | Phase 2: Resolve Planning Questions |
| 291 | H3 | Phase 3: Structure the Plan |
| 293 | H4 | 3.1 Title and File Naming |
| 304 | H4 | 3.2 Stakeholder and Impact Awareness |
| 308 | H4 | 3.3 Break Work into Implementation Units |
| 324 | H4 | 3.4 High-Level Technical Design (Optional) |
| 351 | H4 | 3.4b Output Structure (Optional) |
| 365 | H4 | 3.5 Define Each Implementation Unit |
| 392 | H4 | 3.6 Keep Planning-Time and Implementation-Time Unknowns Separate |
| 402 | H3 | Phase 4: Write the Plan |
| 406 | H4 | 4.1 Plan Depth Guidance |
| 424 | H4 | 4.1b Optional Deep Plan Extensions |
| 438 | H4 | 4.2 Core Plan Template |
| 452 | H1 | [Plan Title] *(inside code block — template)* |
| 454 | H2 | Overview *(inside code block)* |
| 458 | H2 | Problem Frame *(inside code block)* |
| 462 | H2 | Requirements Trace *(inside code block)* |
| 467 | H2 | Scope Boundaries *(inside code block)* |
| 473 | H3 | Deferred to Separate Tasks *(inside code block)* |
| 477 | H2 | Context & Research *(inside code block)* |
| 479 | H3 | Relevant Code and Patterns *(inside code block)* |
| 483 | H3 | Institutional Learnings *(inside code block)* |
| 487 | H3 | External References *(inside code block)* |
| 491 | H2 | Key Technical Decisions *(inside code block)* |
| 495 | H2 | Open Questions *(inside code block)* |
| 497 | H3 | Resolved During Planning *(inside code block)* |
| 501 | H3 | Deferred to Implementation *(inside code block)* |
| 509 | H2 | Output Structure *(inside code block)* |
| 517 | H2 | High-Level Technical Design *(inside code block)* |
| 523 | H2 | Implementation Units *(inside code block)* |
| 555 | H2 | System-Wide Impact *(inside code block)* |
| 564 | H2 | Risks & Dependencies *(inside code block)* |
| 570 | H2 | Documentation / Operational Notes *(inside code block)* |
| 574 | H2 | Sources & References *(inside code block)* |
| 585 | H2 | Alternative Approaches Considered *(inside code block)* |
| 589 | H2 | Success Metrics *(inside code block)* |
| 593 | H2 | Dependencies / Prerequisites *(inside code block)* |
| 597 | H2 | Risk Analysis & Mitigation *(inside code block)* |
| 603 | H2 | Phased Delivery *(inside code block)* |
| 605 | H3 | Phase 1 *(inside code block)* |
| 608 | H3 | Phase 2 *(inside code block)* |
| 611 | H2 | Documentation Plan *(inside code block)* |
| 615 | H2 | Operational / Rollout Notes *(inside code block)* |
| 620 | H4 | 4.3 Planning Rules |
| 632 | H4 | 4.4 Visual Communication in Plan Documents |
| 636 | H3 | Phase 5: Final Review, Write File, and Handoff |
| 638 | H4 | 5.1 Review Before Writing |
| 662 | H4 | 5.2 Write Plan File |
| 680 | H4 | 5.3 Confidence Check and Deepening |
| 697 | H5 | 5.3.1 Classify Plan Depth and Topic Risk |
| 713 | H5 | 5.3.2 Gate: Decide Whether to Deepen |
| 722 | H5 | 5.3.3--5.3.7 Deepening Execution |
| 726 | H5 | 5.3.8--5.4 Document Review, Final Checks, and Post-Generation Options |

**Live document structure headings only (outside code blocks):** 39 headings across H2-H5. The code block template (lines 442-618) contributes 36 heading-like lines but these are content examples, not navigational structure.

---

## 4. Content Specificity Assessment

**Score: 5 / 5**

This skill is maximally operationalized. Every phase includes concrete decision criteria, named conditionals, exact tool invocations, agent names, file path conventions, and word-for-word trigger phrases. It functions as a full finite state machine for a planning workflow, not a general description of what planning involves.

**Justification excerpts:**

1. Line 219-231 -- External research decision criteria are enumerated with explicit signals and named technology thresholds:
   > "Always lean toward external research when: The topic is high-risk: security, payments, privacy, external APIs, migrations, compliance / The codebase lacks relevant local patterns -- fewer than 3 direct examples of the pattern this plan needs / Local patterns exist for an adjacent domain but not the exact one"
   These are not vague heuristics. They name counts, distinguish adjacent from direct patterns, and give specific framing for research queries.

2. Lines 376-381 -- Test scenario specification is enumerated to the category level with a rule for when each category is required vs. optional:
   > "Happy path behaviors -- core functionality with expected inputs and outputs / Edge cases (when the unit has meaningful boundaries) -- boundary values, empty inputs, nil/null states, concurrent access / Error and failure paths (when the unit has failure modes) / Integration scenarios (when the unit crosses layers)"
   Each category is conditional on the unit's actual properties, not required universally.

3. Lines 65-76 -- Deepening trigger logic defines precise inclusion and exclusion criteria:
   > "Words like 'strengthen', 'confidence', 'gaps', and 'rigor' are NOT sufficient on their own to trigger deepening... Only treat them as deepening intent when the request clearly targets the plan as a whole and does not name a specific section or content area to change -- and even then, prefer to confirm with the user before entering the deepening flow."
   This is disambiguation code, not guidance.

---

## 5. Internal File References

All four `references/` files are explicitly loaded conditionally, not eagerly. Each load is gated on a specific runtime condition:

| Reference file | Load condition | SKILL.md line |
|---|---|---|
| `references/universal-planning.md` | Phase 0.1b: task classified as non-software domain | 82 |
| `references/universal-planning.md` | Phase 0.1: plan lacks YAML frontmatter (non-software deepen) | 71 |
| `references/deepening-workflow.md` | Phase 5.3.3--5.3.7: deepening gate determines strengthening is warranted | 724 |
| `references/plan-handoff.md` | Phase 5.3.8--5.4: after plan file is written and confidence check complete | 728 |
| `references/visual-communication.md` | Section 4.4: plan has 4+ units with non-linear deps, 3+ interacting surfaces, etc. | 634 |

Other path references (within prose or templates, not file loads):
- `docs/brainstorms/` -- upstream requirements document location (Phase 0.2)
- `docs/plans/` -- plan output directory (Phase 3.1, 5.2)
- `docs/solutions/` -- institutional learnings (Phase 1.4)
- `.context/compound-engineering/ce-plan/deepen/` -- artifact-backed mode scratch directory (referenced in deepening-workflow.md)
- `AGENTS.md` -- project guidance consumed in Phase 1.1 and issue creation
- `CLAUDE.md` -- compatibility fallback for AGENTS.md

---

## 6. Skill Cross-References

| Skill | Nature of reference |
|---|---|
| `ce:brainstorm` | Upstream: produces requirements documents consumed by ce:plan. Recommended when product ambiguity is high or scope undefined. Referenced as the preferred entry for exploratory requests. |
| `ce:plan` | Self-reference in description (deepening use case) and frontmatter. |
| `ce:work` | Downstream: executes plans produced by ce:plan. Post-generation option #1 and #5. |
| `document-review` | Post-generation: mandatory quality gate in Phase 5.3.8 after plan file is written. Explicitly distinguished from the confidence check as catching a different class of issues. |
| `proof` | Post-generation: optional upload/share path via plan-handoff.md (Step 4, option 4). |

---

## 7. Agent References

**Agents referenced in SKILL.md (Phase 1 dispatch):**

| Agent | Role | Dispatch condition |
|---|---|---|
| `compound-engineering:research:repo-research-analyst` | Technology, architecture, and patterns scan | Always (Phase 1.1, parallel) |
| `compound-engineering:research:learnings-researcher` | Institutional knowledge from docs/solutions/ | Always (Phase 1.1, parallel) |
| `compound-engineering:research:slack-researcher` | Organizational context | Opt-in only: tools available AND user asked |
| `compound-engineering:research:best-practices-researcher` | External patterns and best practices | Conditional (Phase 1.3) |
| `compound-engineering:research:framework-docs-researcher` | Official framework documentation | Conditional (Phase 1.3) |
| `compound-engineering:workflow:spec-flow-analyzer` | User flow completeness, edge cases, handoff gaps | Standard or Deep plans only (Phase 1.5) |

**Additional agents referenced only in `references/deepening-workflow.md` (Phase 5.3.4 targeted dispatch):**

| Agent | Deepening target sections |
|---|---|
| `compound-engineering:research:git-history-analyzer` | Context & Research gaps (historical rationale) |
| `compound-engineering:review:architecture-strategist` | Key Technical Decisions, High-Level Technical Design, System-Wide Impact |
| `compound-engineering:review:pattern-recognition-specialist` | Implementation Units (consistency, duplication) |
| `compound-engineering:review:performance-oracle` | System-Wide Impact, Risks & Dependencies |
| `compound-engineering:review:security-sentinel` | System-Wide Impact, Risks & Dependencies |
| `compound-engineering:review:data-integrity-guardian` | System-Wide Impact, Risks & Dependencies |
| `compound-engineering:review:data-migration-expert` | Risks & Dependencies (migration realism) |
| `compound-engineering:review:deployment-verification-agent` | Risks & Dependencies (rollout, rollback) |

**Total unique agents across all files:** 14

---

## 8. Other Markdown File Analysis

### references/deepening-workflow.md

| Metric | Value |
|---|---|
| Size | 15,349 bytes |
| Reported lines | ~250 (estimated from size and word density) |

**Content:** Full confidence-gap scoring workflow (sections 5.3.3--5.3.7). Defines checklists for 9 plan sections, section-to-agent deterministic mapping table, three execution modes (direct, artifact-backed), interactive finding review protocol (5.3.6b), and plan synthesis rules (5.3.7). This is the largest reference file and contains the most algorithmic content in the skill system.

**Key structures:** Section checklists (9 sections, 4-6 bullet criteria each), deterministic dispatch mapping table, explicit agent prompt shape instructions, interactive vs. auto mode branching at 5.3.6b.

**Agents referenced:** 13 unique agents (see Section 7 above).

---

### references/plan-handoff.md

| Metric | Value |
|---|---|
| Size | 5,223 bytes |
| Reported lines | ~100 (estimated) |

**Content:** Post-writing instructions covering: mandatory document-review invocation (5.3.8), final quality checks (5.3.9), interactive post-generation options menu (5.4), and issue creation for GitHub and Linear. Contains bash code blocks for Proof upload and gh/linear CLI issue creation.

**Key structures:** Options menu (6 choices), bash command blocks for API calls, tracker detection logic, pipeline mode bypass instructions.

**Skills referenced:** `ce:work`, `document-review`, `proof`.

---

### references/universal-planning.md

| Metric | Value |
|---|---|
| Size | 8,553 bytes |
| Reported lines | ~180 (estimated) |

**Content:** Complete domain-agnostic planning workflow for non-software tasks. Contains domain classification verification, research need assessment table (None / Recommended), focused Q&A guidance, plan format selection table (high personal preference / logical sequence / hybrid), quality principles, and save/share options.

**Key structures:** Research need decision table, format selection table with 3 task types, quality principle list (7 items), Step 3 options menu (save / share to Proof / both).

**Notable:** Pipeline mode has an explicit rejection gate -- outputs a specific error string and stops if invoked from LFG/SLFG, since ce:work does not support non-software tasks.

---

### references/visual-communication.md

| Metric | Value |
|---|---|
| Size | 3,293 bytes |
| Reported lines | ~60 (estimated) |

**Content:** Conditional guidance for plan-structure visual aids (distinct from solution-design diagrams in Section 3.4). Defines inclusion/exclusion criteria for mermaid dependency graphs, interaction diagrams, and markdown comparison tables. Specifies format selection (mermaid vs. ASCII vs. tables) with column-width and node-count guidance.

**Key structures:** Inclusion criteria table (4 conditions), format selection guidance, node count rule (5-15 for mermaid), 80-column max for ASCII. Smallest reference file.

---

## 9. Structural Observations

### YAML Frontmatter

Present and well-formed. Fields:
- `name: ce:plan`
- `description:` (698 chars, includes explicit trigger phrases for invocation routing)
- `argument-hint:` (describes optional argument types)

No `tools`, `model`, or `color` fields. Frontmatter is minimal -- invocation routing is entirely description-based.

### Code Blocks

Three fenced code blocks in SKILL.md:
1. **Core plan template** (lines ~442-618, ~176 lines): Full markdown template for generated plan files including YAML frontmatter schema, all section headings, and per-unit structure. Contains embedded markdown headings (H1-H3) that inflate raw heading counts.
2. **Filename format** (lines ~668-670): Short 3-line block showing plan file path convention.
3. **Plan written confirmation** (lines ~673-676): Short confirmation text block.

Additional code blocks in `references/plan-handoff.md`: bash commands for Proof upload (curl + jq) and issue creation (gh, linear CLI).

### Lists vs. Prose

The skill is primarily prose with embedded lists. Proportions:
- Prose paragraphs: majority of content (~60-65%)
- Bullet lists: frequent, especially in Phase 1 research criteria, Phase 3.5 unit fields, Phase 5.1 review checklist
- Tables: 4 decision tables in SKILL.md (sections 3.4, 4.4 cross-reference); additional tables in reference files
- Numbered lists: Core Principles section (7 items), post-generation options in plan-handoff.md

### Conditional Logic

Extensive and explicit. Conditions are named inline:
- `(Conditional)` suffix on section titles (1.3, 1.5)
- `(Always Runs)` suffix on 1.1
- `(Optional)` suffix on 3.4, 3.4b
- Explicit pipeline mode bypass blocks throughout (Phases 0.1, 5.2, 5.3, 5.4)
- Auto mode vs. interactive mode split for confidence check (Phase 5.3)
- Lightweight/Standard/Deep branching at multiple decision points
- High-risk signal list (Phase 5.3.1) used to override normal depth gating

### Templates

One complete plan document template embedded in Phase 4.2 (core plan template, ~176 lines). A second extension template for Deep plans follows immediately (lines ~582-618). Both are inside fenced code blocks with markdown headings. These templates are the source of truth for what generated plan files look like.

### Examples

Inline examples are used throughout:
- Filename examples: `2026-01-15-001-feat-user-authentication-flow-plan.md`
- File path examples: `src/models/user.rb` (correct) vs. `/Users/name/Code/project/src/models/user.rb` (prohibited)
- Research announcement examples: `"Your codebase has solid patterns for this. Proceeding without external research."`
- Agent dispatch task call examples: `Task compound-engineering:research:repo-research-analyst(Scope: technology, architecture, patterns. {planning context summary})`
- Execution note examples: three concrete `Execution note:` strings (lines 386-388)
- Test scenario prefix examples: Happy path, Edge case, Error path, Integration

### Constraints

Multiple explicit prohibitions enforced in planning rules (Section 4.3) and review checklist (Section 5.1):
- No absolute file paths (enforced in Planning Rules and repeated in Quality Bar, Phase 4.3, Feature Description block)
- No implementation code (no imports, exact method signatures, framework-specific syntax)
- No git commands, commit messages, or test command recipes
- No micro-step RED/GREEN/REFACTOR expansion
- No silent resolution of execution-time questions
- No generic `Research Insights` subsections added during deepening
- No rewriting the entire plan from scratch during deepening
- No inventing new product requirements during deepening
- Feature-bearing units must have actual test scenarios -- `Test expectation: none` is only valid for non-feature-bearing units

The terminal line of SKILL.md is a constraint capsule: `NEVER CODE! Research, decide, and write the plan.`

### Progressive Disclosure / Lazy Loading Pattern

The skill uses a deliberate lazy-loading pattern for its three largest reference files. None are loaded at skill invocation. Each is loaded at a specific phase gate:
- `universal-planning.md` -- loaded only if non-software classification confirmed (Phase 0.1b or 0.1 for non-software deepen)
- `deepening-workflow.md` -- loaded only if deepening gate passes (Phase 5.3.3)
- `plan-handoff.md` -- loaded only after plan file is written (Phase 5.3.8)
- `visual-communication.md` -- loaded only when visual aid conditions are met (Section 4.4)

This pattern keeps the active context window minimal for simple use cases (a lightweight software plan never loads three of the four reference files) and maximizes token budget for the actual planning work.
