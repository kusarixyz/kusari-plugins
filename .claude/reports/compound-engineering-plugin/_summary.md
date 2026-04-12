# Aggregate Skill Analysis: EveryInc/compound-engineering-plugin (First 10)

**Repository:** EveryInc/compound-engineering-plugin  
**Branch:** main  
**Skills analyzed:** 10 of 40  
**Analysis date:** 2026-04-11

---

## Scale

| Metric | Value |
|--------|-------|
| Skills analyzed | 10 |
| Total files across all skills | 56 |
| Total estimated tokens (SKILL.md files only) | ~43,443 |
| Total bytes across all skill files | ~497,000+ |

---

## SKILL.md Size Distribution

| Metric | Min | Median | Max |
|--------|-----|--------|-----|
| **Line count** | ~99 (ce-demo-reel) | ~210 (mcp range) | 730 (ce-plan) |
| **Word count** | ~620 (andrew-kane-gem-writer) | ~1,939 (ce-debug) | ~7,405 (ce-compound-refresh) |
| **Token estimate** | ~827 (andrew-kane-gem-writer) | ~2,585 (ce-debug) | ~9,873 (ce-compound-refresh) |
| **Character count** | 4,689 (andrew-kane-gem-writer) | 11,219 (midpoint) | 48,110 (ce-compound-refresh) |

### Size tiers

- **Small (<2,000 tokens):** andrew-kane-gem-writer (827), agent-native-audit (1,699), ce-demo-reel (1,716), ce-ideate (1,967)
- **Medium (2,000-5,000 tokens):** ce-debug (2,585), ce-brainstorm (2,776), agent-native-architecture (4,600)
- **Large (5,000+ tokens):** ce-compound (8,304), ce-plan (8,391), ce-compound-refresh (9,873)

The distribution is more top-heavy than anthropics/skills. Three skills exceed 8,000 tokens in SKILL.md alone. The median is significantly larger than anthropics/skills (2,585 vs 1,720).

---

## Structure Depth

| Max heading depth | Count | Skills |
|-------------------|-------|--------|
| H2 only | 2 | andrew-kane-gem-writer, ce-demo-reel |
| H3 | 2 | agent-native-architecture, agent-native-audit |
| H4 | 5 | ce-brainstorm, ce-compound, ce-compound-refresh, ce-debug, ce-ideate |
| H5 | 1 | ce-plan |

**Most common:** H4 (5/10 skills). This is deeper than anthropics/skills where H3 dominates. The compound-engineering plugin favors deeper heading hierarchies for its phased workflows.

### Heading counts

| Metric | Min | Median | Max |
|--------|-----|--------|-----|
| Total headings | 10 (ce-ideate) | 28.5 | 75 (ce-plan, including template) |

---

## Content Specificity Distribution

| Score | Count | Skills |
|-------|-------|--------|
| 3 (mixed) | 1 | agent-native-audit |
| 3.5 | 1 | agent-native-architecture |
| 4 (mostly specific) | 1 | ce-ideate |
| 5 (extremely granular) | 7 | andrew-kane-gem-writer, ce-brainstorm, ce-compound, ce-compound-refresh, ce-debug, ce-demo-reel, ce-plan |

**Dominant pattern:** 5/5. Seven of ten skills are at maximum specificity. This is a stark contrast to anthropics/skills where only 5/17 scored 5. The compound-engineering plugin is overwhelmingly operationally prescriptive.

---

## Cross-Referencing Patterns

### Skill-to-skill references

**8 out of 10 skills reference other skills.** This is the opposite of anthropics/skills where 0/17 had cross-references. The compound-engineering plugin forms an interconnected graph:

| Skill | References to |
|-------|--------------|
| agent-native-audit | agent-native-architecture |
| ce-brainstorm | document-review, ce:plan, ce:brainstorm (self) |
| ce-compound | ce:compound-refresh, ce:plan |
| ce-compound-refresh | ce:compound, ce:brainstorm |
| ce-debug | /proof, ce:brainstorm, ce:compound |
| ce-demo-reel | git-commit-push-pr |
| ce-ideate | ce:brainstorm, ce:plan |
| ce-plan | ce:brainstorm, ce:work, document-review, proof |

Only agent-native-architecture and andrew-kane-gem-writer are fully self-contained.

### Agent references

**7 out of 10 skills reference agents.** Agent dispatch is a core architectural pattern:

| Skill | Agent count | Pattern |
|-------|------------|---------|
| agent-native-audit | 8 (inline sub-agents) | Parallel Task-tool dispatch with Explore type |
| ce-brainstorm | 1 named (slack-researcher) | Conditional opt-in dispatch |
| ce-compound | 11 (3 research + 8 review) | Parallel Phase 1, conditional Phase 3 |
| ce-compound-refresh | 2 roles (investigation + replacement) | Read-only parallel + sequential write |
| ce-debug | 1 (agent-browser) | Conditional with fallback chain |
| ce-ideate | 3 named research agents + 1 anonymous | Multi-tier model dispatch |
| ce-plan | 14 unique agents | Phase-gated, depth-conditional dispatch |

ce-plan has the largest agent surface (14 unique agents across all files).

### Referencing mechanisms

- **Colon-namespaced identifiers:** `compound-engineering:research:learnings-researcher` (dominant pattern)
- **Slash-command syntax:** `/ce:brainstorm`, `/ce:plan`, `/proof`
- **Platform tool names:** `AskUserQuestion` / `request_user_input` / `ask_user` (multi-platform pattern)
- **XML structural markers:** `<parallel_tasks>`, `<sequential_tasks>`, `<critical_requirement>` (ce-compound)

---

## File Composition

| Metric | Min | Median | Max |
|--------|-----|--------|-----|
| Files per skill | 1 (agent-native-audit) | 4 | 15 (agent-native-architecture) |
| Subdirectories | 0 (agent-native-audit) | 1 | 2 |

### Common directory pattern

Every skill with supplementary files uses `references/` as the primary subdirectory. `assets/` appears in 2 skills (ce-compound, ce-compound-refresh) for document templates. `scripts/` appears in 1 skill (ce-demo-reel) for a Python automation helper.

### Supplementary markdown files

| Has supplementary .md files | Count |
|-----------------------------|-------|
| Yes | 8 |
| No | 2 (agent-native-audit, only SKILL.md) |

Average reference file count among skills with references: 3.6 files.

---

## Title and Description Lengths

### Title

| Metric | Value |
|--------|-------|
| Min | 9 chars (ce-compound: `/compound`, ce-demo-reel: `Demo Reel`) |
| Median | 21 chars |
| Max | 38 chars (ce-brainstorm: `Brainstorm a Feature or Improvement`) |

### Description

| Metric | Value |
|--------|-------|
| Min | 67 chars (ce-compound) |
| Median | 396 chars |
| Max | 698 chars (ce-plan) |

Descriptions are consistently longer than anthropics/skills (median 396 vs 318). Most descriptions embed explicit trigger phrases and negative conditions.

---

## Structural Conventions

### YAML frontmatter fields

| Field | Prevalence |
|-------|-----------|
| `name` | 10/10 |
| `description` | 10/10 |
| `argument-hint` | 6/10 |
| `disable-model-invocation` | 2/10 (agent-native-audit, ce-compound-refresh) |

The `argument-hint` field is a distinctive convention not found in anthropics/skills. `disable-model-invocation: true` is used for skills that perform destructive operations or rely entirely on sub-agent orchestration.

### Phase-based workflow structure

**8 out of 10 skills use numbered phases** (Phase 0, 1, 2, ...). This is the dominant organizational pattern. Two skills (agent-native-architecture, andrew-kane-gem-writer) use flat H2 sections instead.

Phase numbering conventions:
- Non-integer phases (1.5, 1.75) in ce-compound-refresh indicate post-design insertions
- Sub-phase numbering (0.1, 0.1b, 0.2, 1.1, 1.2) in ce-brainstorm, ce-plan, ce-ideate
- Phase 0 universally handles resume/routing/triage

### Common heading patterns across skills

- **Core Principles** -- 5 skills (ce-brainstorm, ce-debug, ce-plan, ce-compound, ce-compound-refresh)
- **Interaction Rules / Method** -- 4 skills
- **Execution Flow / Workflow** -- 8 skills
- **Phase 0: Resume / Assess / Route** -- 5 skills
- **Discoverability Check** -- 2 skills (ce-compound, ce-compound-refresh)
- **Output / Output Format** -- 4 skills

### Content patterns

| Pattern | Count | Notes |
|---------|-------|-------|
| Code blocks present | 9/10 | Only ce-ideate has zero code blocks in SKILL.md |
| Decision tables | 5/10 | ce-debug, ce-compound, ce-compound-refresh, ce-plan, ce-demo-reel |
| Platform-specific tool names | 7/10 | `AskUserQuestion`/`request_user_input`/`ask_user` triple |
| Explicit prohibitions | 10/10 | Average 6-7 per skill |
| Conditional branching | 9/10 | Only andrew-kane-gem-writer has none |
| Lazy-loading of reference files | 7/10 | Dominant context management pattern |
| Resume/continuation logic | 5/10 | Check for prior work at Phase 0 |
| Scope tiering (Lightweight/Standard/Deep) | 4/10 | ce-brainstorm, ce-compound, ce-plan, ce-compound-refresh |
| Subagent orchestration | 7/10 | Parallel + sequential dispatch patterns |
| XML structural markers | 1/10 | Only ce-compound |

---

## Architectural Patterns

### 1. Phased workflow orchestrator (7/10)

SKILL.md defines a sequential phase pipeline with conditional branching, subagent dispatch, and lazy-loaded reference files. This is the dominant pattern.

**Skills:** ce-brainstorm, ce-compound, ce-compound-refresh, ce-debug, ce-demo-reel, ce-ideate, ce-plan

### 2. Sub-agent manifest (1/10)

SKILL.md is primarily a collection of inline sub-agent prompt templates dispatched via the Task tool. The skill itself does minimal work.

**Skills:** agent-native-audit

### 3. Knowledge reference with interactive routing (1/10)

SKILL.md presents conceptual content with an interactive menu that gates access to a large reference corpus.

**Skills:** agent-native-architecture

### 4. Static knowledge module (1/10)

SKILL.md contains domain-specific patterns and conventions with no workflow logic, no phases, no agents.

**Skills:** andrew-kane-gem-writer

---

## Lazy-Loading Pattern (Distinctive Design)

The most structurally distinctive pattern in this plugin is **systematic lazy-loading of reference files**. 7/10 skills explicitly defer loading reference content until a specific phase gate is reached. This is implemented via prose instructions like:

> "Read `references/post-ideation-workflow.md` for the adversarial filtering rubric... Do not load this file before Phase 2 agent dispatch completes."

This pattern serves two purposes:
1. **Context window conservation** -- avoids front-loading 10,000+ tokens of reference material
2. **Conditional paths** -- some reference files are only needed for specific branches (e.g., non-software tasks, deep plans, specific tiers)

In contrast, anthropics/skills loads reference content at the point of use but does not explicitly enforce deferred loading as a stated constraint.

---

## Comparison with anthropics/skills

| Dimension | anthropics/skills (17) | compound-engineering (10) |
|-----------|----------------------|--------------------------|
| Median SKILL.md tokens | 1,720 | 2,585 |
| Max SKILL.md tokens | 6,293 | 9,873 |
| Skills at specificity 5 | 5/17 (29%) | 7/10 (70%) |
| Cross-skill references | 0/17 | 8/10 |
| Agent references | 1/17 | 7/10 |
| Phase-based workflow | 0/17 | 8/10 |
| Lazy-loading pattern | 3/17 (implicit) | 7/10 (explicit) |
| `disable-model-invocation` | 0/17 | 2/10 |
| Platform-specific tool names | 0/17 | 7/10 |
| Binary assets | 3/17 | 0/10 |
| Scripts | 10/17 | 1/10 |

The two repositories represent fundamentally different skill philosophies:

- **anthropics/skills** builds self-contained reference modules. Each skill is a standalone knowledge unit with scripts for automation. Cross-skill coupling is zero. Agent integration is minimal. The primary pattern is "give the model all the knowledge it needs to do the job."

- **compound-engineering** builds interconnected workflow orchestrators. Skills form a graph of handoffs. Agent dispatch is pervasive. The primary pattern is "define a deterministic workflow that the model executes step by step, dispatching specialized agents at each phase."
