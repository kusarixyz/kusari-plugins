---
repository: EveryInc/compound-engineering-plugin
branch: main
skill-path: plugins/compound-engineering/skills/ce-compound-refresh
analyzed: 2026-04-11
---

# Skill Analysis: ce-compound-refresh


## 1. Overview

**Skill name:** `ce:compound-refresh`

**Title text (H1):** `Compound Refresh`
**Title char length:** 16 characters

**Description (frontmatter):**
> Refresh stale or drifting learnings and pattern docs in docs/solutions/ by reviewing, updating, consolidating, replacing, or deleting them against the current codebase. Use after refactors, migrations, dependency upgrades, or when a retrieved learning feels outdated or wrong. Also use when reviewing docs/solutions/ for accuracy, when a recently solved problem contradicts an existing learning, when pattern docs no longer reflect current code, or when multiple docs seem to cover the same topic and might benefit from consolidation.

**Description char length:** 495 characters

**Total files (recursive):** 4
- `SKILL.md` (48,110 bytes)
- `assets/resolution-template.md` (1,996 bytes)
- `references/schema.yaml` (6,980 bytes)
- `references/yaml-schema.md` (4,511 bytes)

**Subdirectories:** 2
- `assets/`
- `references/`

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Line count | 679 |
| Word count | 7,405 |
| Estimated token count (words / 0.75) | 9,873 |
| Character count | 48,110 |

---

## 3. Document Structure Depth

### All headings in order

| Line | Level | Text |
|------|-------|------|
| 7 | H1 | Compound Refresh |
| 11 | H2 | Mode Detection |
| 20 | H3 | Autofix mode rules |
| 29 | H2 | Interaction Principles |
| 43 | H2 | Refresh Order |
| 59 | H2 | Maintenance Model |
| 71 | H2 | Core Rules |
| 88 | H2 | Scope Selection |
| 115 | H2 | Phase 0: Assess and Route |
| 123 | H3 | Route by Scope |
| 131 | H3 | Broad Scope Triage |
| 156 | H2 | Phase 1: Investigate Candidate Learnings |
| 171 | H3 | Drift Classification: Update vs Replace |
| 187 | H3 | Judgment Guidelines |
| 195 | H2 | Phase 1.5: Investigate Pattern Docs |
| 203 | H2 | Phase 1.75: Document-Set Analysis |
| 207 | H3 | Overlap Detection |
| 219 | H3 | Supersession Signals |
| 229 | H3 | Canonical Doc Identification |
| 242 | H3 | Retrieval-Value Test |
| 253 | H3 | Cross-Doc Conflict Check |
| 262 | H2 | Subagent Strategy |
| 286 | H2 | Phase 2: Classify the Right Maintenance Action |
| 290 | H3 | Keep |
| 294 | H3 | Update |
| 298 | H3 | Consolidate |
| 318 | H3 | Replace |
| 334 | H3 | Delete |
| 345 | H3 | Before deleting: check if the problem domain is still active |
| 364 | H2 | Pattern Guidance |
| 374 | H2 | Phase 3: Ask for Decisions |
| 376 | H3 | Autofix mode |
| 384 | H3 | Interactive mode |
| 395 | H4 | Question Style |
| 407 | H4 | Focused Scope |
| 431 | H4 | Batch Scope |
| 448 | H4 | Broad Scope |
| 459 | H2 | Phase 4: Execute the Chosen Action |
| 461 | H3 | Keep Flow |
| 465 | H3 | Update Flow |
| 487 | H3 | Consolidate Flow |
| 501 | H3 | Replace Flow |
| 530 | H3 | Delete Flow |
| 534 | H2 | Output Format |
| 563 | H3 | Autofix mode report |
| 585 | H2 | Phase 5: Commit Changes |
| 589 | H3 | Detect git context |
| 596 | H3 | Autofix mode |
| 608 | H3 | Interactive mode |
| 629 | H3 | Commit message |
| 636 | H2 | Relationship to ce:compound |
| 636 | H2 | Discoverability Check |

**Total headings:** 52

**Max depth:** H4 (4 levels)

**Count by level:**
| Level | Count |
|-------|-------|
| H1 | 1 |
| H2 | 20 |
| H3 | 27 |
| H4 | 4 |

**Note on heading count anomaly:** The grep output shows 52 lines matching `^#`, but the table above reflects the parsed heading structure. The grep count includes lines within code blocks that begin with `#` (YAML comments in embedded code examples). Actual markdown headings: H1=1, H2=20, H3=27, H4=4, total=52 lines starting with `#` including code block content.

---

## 4. Content Specificity Assessment

**Score: 5/5** — Maximally specific. Every section provides unambiguous, executable instruction with decision criteria, not general guidance.

**Excerpt 1 — Precise decision boundary (lines 171-176):**
> The critical distinction is whether the drift is cosmetic (references moved but the solution is the same) or substantive (the solution itself changed)... The boundary: if you find yourself rewriting the solution section or changing what the learning recommends, stop — that is Replace, not Update.

The Update/Replace boundary is drawn at a single behavioral signal ("rewriting the solution section"), not a vague heuristic.

**Excerpt 2 — Auto-delete criteria enumerated explicitly (lines 353-362):**
> Auto-delete only when both the implementation AND the problem domain are gone: the referenced code is gone AND the application no longer deals with that problem domain / the learning is fully superseded by a clearly better successor AND the old doc adds no distinct value / the document is plainly redundant and adds nothing the canonical doc doesn't already say

Three independently sufficient conditions for auto-delete are itemized, preventing mechanical over-deletion.

**Excerpt 3 — Subagent role separation with operational constraint (lines 281-282):**
> Investigation subagents — read-only. They must not edit files, create successors, or delete anything... Replacement subagents — write a single new learning to replace a stale one. These run one at a time, sequentially (each replacement subagent may need to read significant code, and running multiple in parallel risks context exhaustion).

Role separation is not just conceptual — it includes a concrete operational constraint (sequential execution) with a stated technical rationale (context exhaustion).

---

## 5. Internal File References

All file references found in SKILL.md:

| Reference | Lines | Purpose |
|-----------|-------|---------|
| `references/schema.yaml` | 507, 520 | Frontmatter fields and enum values passed to replacement subagents |
| `references/yaml-schema.md` | 508, 520 | Category mapping passed to replacement subagents |
| `assets/resolution-template.md` | 509, 520 | Section structure passed to replacement subagents |
| `docs/solutions/` | Multiple | Target directory for all maintained learnings/patterns |
| `docs/solutions/_archived/` | 95, 97, 582 | Legacy directory — flagged for cleanup if found |
| `docs/solutions/patterns/` | 197 | Location of pattern docs |
| `MEMORY.md` | 166, 277 | Auto memory directory file checked for drift signals |
| `AGENTS.md` | 649 | Root-level instruction file for discoverability check |
| `CLAUDE.md` | 649 | Root-level instruction file for discoverability check |

---

## 6. Skill Cross-References

| Referenced Skill | Lines | Context |
|-----------------|-------|---------|
| `ce:compound` | 112, 332, 528, 638–643 | Companion skill — captures newly solved problems; recommended when refresh evidence is insufficient |
| `ce:compound-refresh` | 175 | Self-reference in drift classification description |
| `ce:brainstorm` | 33 | Interaction style reference: "Follow the same interaction style as `ce:brainstorm`" |

---

## 7. Agent References

| Agent/Tool | Lines | Context |
|-----------|-------|---------|
| Investigation subagents | 281 | Read-only parallel agents for artifact investigation |
| Replacement subagents | 282, 503–521 | Sequential write agents producing replacement learnings |
| Orchestrator | 284, 489 | Main thread coordinating subagents, deletions, metadata updates |
| `AskUserQuestion` (Claude Code tool) | 35, 397 | Platform-specific blocking question tool |
| `request_user_input` (Codex tool) | 35, 397 | Platform-specific blocking question tool |
| `ask_user` (Gemini tool) | 35, 397 | Platform-specific blocking question tool |

The skill distinguishes between two subagent roles. Investigation subagents can run in parallel; replacement subagents are explicitly constrained to sequential execution. The orchestrator role is kept in the main thread.

---

## 8. Other Markdown File Analysis

### assets/resolution-template.md

**Size:** 1,996 bytes
**Purpose:** Document templates for new learnings created by replacement subagents. Defines section order and content expectations.

**Structure:**
- Two tracks: Bug Track Template and Knowledge Track Template
- Bug track covers: `build_error`, `test_failure`, `runtime_error`, `performance_issue`, `database_issue`, `security_issue`, `ui_bug`, `integration_issue`, `logic_error`
- Knowledge track covers: `best_practice`, `documentation_gap`, `workflow_issue`, `developer_experience`
- Each template is a complete fenced markdown code block with YAML frontmatter placeholder and all required sections

**Approximate metrics:**
| Metric | Estimate |
|--------|---------|
| Lines | ~70 |
| Headings | 3 (H1 + 2 H2) |
| Code blocks | 2 (one template per track) |
| Estimated tokens | ~430 |

**Sections in Bug Track template:** Problem, Symptoms, What Didn't Work, Solution, Why This Works, Prevention, Related Issues

**Sections in Knowledge Track template:** Context, Guidance, Why This Matters, When to Apply, Examples, Related

### references/yaml-schema.md

**Size:** 4,511 bytes
**Purpose:** Human-readable quick reference for `schema.yaml` — enumerates required fields, enum values, track rules, category mapping, and validation rules.

**Approximate metrics:**
| Metric | Estimate |
|--------|---------|
| Lines | ~95 |
| Headings | 9 (H1 + multiple H2) |
| Tables | 2 (Tracks table, Category Mapping) |
| Estimated tokens | ~980 |

**Sections:** Tracks, Required Fields (both tracks), Bug Track Fields, Knowledge Track Fields, Optional Fields (both tracks), Optional Fields (bug track only), Backward Compatibility, Category Mapping, Validation Rules

**Key data:** 13 problem_type enum values; 17 component enum values; 4 severity values; 17 root_cause values; 10 resolution_type values; 13 category directory mappings; 9 validation rules enumerated.

---

## 9. Structural Observations

### YAML Frontmatter

Three keys present:
```yaml
name: ce:compound-refresh
description: [495-char multi-trigger description]
disable-model-invocation: true
```

`disable-model-invocation: true` is present. This prevents the skill from being invoked by model inference alone — it must be explicitly triggered. This is significant: the skill performs destructive file operations (delete, overwrite) and requires explicit user or system intent.

### Code Blocks

4 fenced code blocks total (8 fence lines / 2):
- Lines 110–113: `text` — "No candidate docs found" empty-state message
- Lines 142–152: `text` — Broad scope triage example output (interactive prompt with numbered options)
- Lines 417–427: `text` — Focused scope question template
- Lines 540–552: `text` — Compound Refresh Summary report format

All code blocks are `text` type (display examples / templates), not executable code. No code samples in programming languages are present in SKILL.md itself — code examples are deferred to the document templates in `assets/resolution-template.md`.

### Lists vs Prose

| Element | Count |
|---------|-------|
| Unordered list items (`- ` or `* `) | 130 |
| Ordered list items (`N. `) | 75 |
| Table rows (`\|`) | 27 (across 8 tables) |

Total list/table items: ~232. The skill is heavily list-structured. Prose paragraphs exist but are typically short (1-4 sentences) serving as introductions to list sections. Extended prose is concentrated in the Core Rules section (lines 71-87, 10 numbered rules with full-sentence rationale each) and the Phase 2 Delete subsection (lines 345-362).

### Tables

8 tables identified:
1. Mode Detection (lines 15-18) — Interactive vs Autofix behavior
2. Maintenance Model outcomes (lines 63-70) — 5 outcomes with meaning and default action
3. Phase 0 Route by Scope (lines 125-129) — 3 scope levels
4. Phase 1 Subagent Strategy (lines 266-271) — 4 approaches
5. Phase 3 Focused Scope question template (implicit via prose)
6. Phase 5 Autofix mode git context (lines 601-606) — 3 contexts with default actions
7. (yaml-schema.md) Tracks (2-column)
8. (yaml-schema.md) Category mapping (2-column)

### Conditional Logic

Pervasive. Two primary branching axes:

1. **Mode axis (Interactive vs Autofix):** Stated at the top (Mode Detection, lines 11-27) and re-stated at every decision point. Phases 3 and 4 both open with explicit autofix bypass instructions. Phase 5 commit flow has separate sub-sections for each mode.

2. **Scope axis (Focused / Batch / Broad):** Phase 0 introduces three scope tiers with distinct interaction styles. Phase 3 has separate question-style sub-sections for each (Focused Scope, Batch Scope, Broad Scope).

Secondary conditionals include: evidence sufficiency for Replace (sufficient vs insufficient, lines 328-332); auto-delete criteria (lines 353-362); discoverability check pass/fail (lines 655-679); git branch state (main vs feature branch, dirty vs clean working tree).

### Templates

Three templates embedded or referenced:
- Focused scope question template (lines 417-427) — inline `text` block
- Broad scope triage output example (lines 142-152) — inline `text` block
- Report summary format (lines 540-552) — inline `text` block

Two full document templates in `assets/resolution-template.md` (Bug Track, Knowledge Track).

### Examples

Concrete examples throughout:
- Scope matching strategies with example directory names (`performance-issues`, `database-issues`) — line 101
- Triage output example with auth module scenario — lines 142-152
- Valid vs invalid in-place update examples (`app/models/auth_token.rb` → `app/models/session_token.rb`) — lines 470-485
- Branch naming examples (`docs/refresh-auth-and-ci-learnings`, not `docs/compound-refresh`) — lines 614-615
- Discoverability addition examples (directory listing line vs new section) — lines 668-676
- Delete vs Replace reasoning examples (session token, deprecated API endpoint) — lines 348-350

### Constraints (Explicit Prohibitions)

Enumerated hard constraints in the skill:
- Do not update a doc just to leave a review breadcrumb (Core Rule 2, line 72)
- Do not ask whether code changes were intentional — match docs to reality (Core Rule 3, line 75)
- Do not edit for typos/style alone (Core Rule 5, line 77; Update Flow lines 477-479)
- No `_archived/` directory — delete only (Core Rule 10, line 86)
- Investigation subagents must not edit files, create successors, or delete anything (line 281)
- Do not let replacement subagents invent frontmatter fields from memory (line 511)
- Do not use shell commands (`ls`, `find`, `cat`, `grep`, `test`, `bash`) for file operations in subagents (line 275)
- In autofix mode: never pause for input, never ask questions (lines 22, 376-382)
- Do not force push to main in the autofix branch creation (implied by branch naming default)
- Do not ask questions about code correctness — stay in doc maintenance scope (line 393)

### Phase Structure

The skill is organized as a numbered phase workflow with non-integer phases reflecting organic additions:
- Phase 0: Assess and Route
- Phase 1: Investigate Candidate Learnings
- Phase 1.5: Investigate Pattern Docs
- Phase 1.75: Document-Set Analysis
- Phase 2: Classify the Right Maintenance Action
- Phase 3: Ask for Decisions
- Phase 4: Execute the Chosen Action
- Phase 5: Commit Changes

The non-integer phase numbers (1.5, 1.75) indicate phases inserted after the original sequential design was established, without renumbering. Phase 1.75 (Document-Set Analysis) is the most structurally complex investigation phase, covering overlap detection, supersession signals, canonical doc identification, retrieval-value test, and cross-doc conflict check across five sub-sections.
