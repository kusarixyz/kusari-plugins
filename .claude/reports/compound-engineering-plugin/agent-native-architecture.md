# Skill Analysis: agent-native-architecture

**Repository:** EveryInc/compound-engineering-plugin
**Branch:** main
**Skill path:** plugins/compound-engineering/skills/agent-native-architecture
**Analysis date:** 2026-04-11

---

## 1. Overview

**Skill name:** `agent-native-architecture`

**Title text (from frontmatter `name` field):** `agent-native-architecture`
- Character length: 27

**Description text:**
> Build applications where agents are first-class citizens. Use this skill when designing autonomous agents, creating MCP tools, implementing self-modifying systems, or building apps where features are outcomes achieved by agents operating in a loop.
- Character length: 247

**Total files (recursive):** 15
- SKILL.md (root)
- 14 files in `references/`

**Subdirectories:** 1 (`references/`)

**File list (with sizes from GitHub API):**

| File | Size (bytes) |
|------|-------------|
| SKILL.md | 22,430 |
| references/action-parity-discipline.md | 11,128 |
| references/agent-execution-patterns.md | 13,317 |
| references/agent-native-testing.md | 16,749 |
| references/architecture-patterns.md | 17,241 |
| references/dynamic-context-injection.md | 9,612 |
| references/files-universal-interface.md | 10,092 |
| references/from-primitives-to-domain-tools.md | 11,788 |
| references/mcp-tool-design.md | 15,658 |
| references/mobile-patterns.md | 25,629 |
| references/product-implications.md | 12,976 |
| references/refactoring-to-prompt-native.md | 8,560 |
| references/self-modification.md | 7,866 |
| references/shared-workspace-architecture.md | 20,874 |
| references/system-prompt-design.md | 6,522 |
| **Total** | **210,442** |

---

## 2. SKILL.md Metrics

All figures derived from the 22,430-byte raw file.

| Metric | Value |
|--------|-------|
| Character count (bytes, UTF-8) | 22,430 |
| Estimated line count | ~430 |
| Estimated word count | ~3,450 |
| Estimated token count (words / 0.75) | ~4,600 |

**Methodology note:** WebFetch returned processed markdown. The byte count is from the GitHub API `size` field on the blob (22,430), which is the authoritative raw byte count. Word and line estimates are derived from the rendered content length and document structure.

---

## 3. Document Structure Depth

### All headings in order with level and line number estimates

| # | Level | Heading Text | Notes |
|---|-------|--------------|-------|
| 1 | H2 | Why Now | First content section |
| 2 | H2 | Core Principles | |
| 3 | H3 | 1. Parity | |
| 4 | H3 | 2. Granularity | |
| 5 | H3 | 3. Composability | |
| 6 | H3 | 4. Emergent Capability | |
| 7 | H3 | 5. Improvement Over Time | |
| 8 | H2 | What Aspect of Agent-Native Architecture Do You Need Help With? | Interactive routing menu |
| 9 | H2 | Routing | Dispatch table |
| 10 | H2 | Architecture Review Checklist | |
| 11 | H3 | Core Principles | Sub-section of checklist |
| 12 | H3 | Tool Design | Sub-section of checklist |
| 13 | H3 | Files & Workspace | Sub-section of checklist |
| 14 | H3 | Agent Execution | Sub-section of checklist |
| 15 | H3 | Context Injection | Sub-section of checklist |
| 16 | H3 | UI Integration | Sub-section of checklist |
| 17 | H3 | Mobile (if applicable) | Sub-section of checklist |
| 18 | H2 | Quick Start: Build an Agent-Native Feature | |
| 19 | H2 | Reference Files | |
| 20 | H2 | Anti-Patterns | |
| 21 | H3 | Common Approaches That Aren't Fully Agent-Native | |
| 22 | H3 | Specific Anti-Patterns | |
| 23 | H2 | Success Criteria | |
| 24 | H3 | Architecture | Sub-section of success criteria |
| 25 | H3 | Implementation | Sub-section of success criteria |
| 26 | H3 | Product | Sub-section of success criteria |
| 27 | H3 | Mobile (if applicable) | Sub-section of success criteria |
| 28 | H3 | The Ultimate Test | Final section |

**Max depth:** H3 (3 levels: document > H2 > H3)

**Count per level:**
- H2: 9
- H3: 19
- H4+: 0

**Total headings:** 28

---

## 4. Content Specificity Assessment

**Scale:** 1 = high-level principles only, 5 = extremely granular (exact values, implementation code, step-by-step procedures)

**Rating: 3.5**

The SKILL.md occupies middle ground, tending toward the specific end. It defines five named principles with concrete tests for each, provides an interactive routing menu with exact response-to-file mappings, includes a multi-category architecture checklist with 25+ binary items, a TypeScript Quick Start with three labeled code steps, and anti-pattern sections with named failure modes. However, it delegates deep implementation detail entirely to reference files rather than embedding it. The SKILL.md is a navigational and conceptual layer with enough specificity to orient the agent, not a complete implementation guide.

**Excerpt justifications:**

1. Specificity evidence (routing table, H2 "Routing"):
   > `| 1, "design", "architecture", "plan" | Read references/architecture-patterns.md, then apply Architecture Checklist below |`
   Exact string triggers mapped to exact file paths. This is operational, not conceptual.

2. Specificity evidence (Quick Start, H2 "Quick Start: Build an Agent-Native Feature"):
   > `const tools = [ tool("read_file", "Read any file", { path: z.string() }, ...), tool("complete_task", "Signal task completion", { summary: z.string() }, ...), ];`
   Named TypeScript tool constructors with typed schemas. Concrete enough to copy directly.

3. Abstraction evidence (H3 "5. Improvement Over Time"):
   > "The improvement mechanisms are still being discovered. Context and prompt refinement are proven. Self-modification is emerging."
   Deliberately hedged. No code, no schema, no step count. Pointing to a direction, not a procedure.

---

## 5. Internal File References

All `references/` paths mentioned in SKILL.md:

| Referenced path | Location | Exists in repo | Context |
|----------------|----------|---------------|---------|
| `references/architecture-patterns.md` | Routing table, Reference Files list | Yes (17,241 bytes) | Route target for "design/architecture/plan" |
| `references/files-universal-interface.md` | Routing table, Reference Files list | Yes (10,092 bytes) | Route target for "files/workspace/filesystem" |
| `references/shared-workspace-architecture.md` | Routing table, Reference Files list | Yes (20,874 bytes) | Route target for "files/workspace/filesystem" |
| `references/mcp-tool-design.md` | Routing table, Reference Files list | Yes (15,658 bytes) | Route target for "tool/mcp/primitive/crud" |
| `references/from-primitives-to-domain-tools.md` | Routing table, Reference Files list | Yes (11,788 bytes) | Route target for "domain tool/when to add" |
| `references/agent-execution-patterns.md` | Routing table, Reference Files list | Yes (13,317 bytes) | Route target for "execution/completion/loop" |
| `references/system-prompt-design.md` | Routing table, Reference Files list | Yes (6,522 bytes) | Route target for "prompt/system prompt/behavior" |
| `references/dynamic-context-injection.md` | Routing table, Reference Files list | Yes (9,612 bytes) | Route target for "context/inject/runtime/dynamic" |
| `references/action-parity-discipline.md` | Routing table, Reference Files list | Yes (11,128 bytes) | Route target for "parity/ui action/capability map" |
| `references/self-modification.md` | Routing table, Reference Files list | Yes (7,866 bytes) | Route target for "self-modify/evolve/git" |
| `references/product-implications.md` | Routing table, Reference Files list | Yes (12,976 bytes) | Route target for "product/progressive/approval/latent demand" |
| `references/agent-native-testing.md` | Routing table, Reference Files list | Yes (16,749 bytes) | Route target for "test/testing/verify/validate" |
| `references/mobile-patterns.md` | Routing table, Reference Files list | Yes (25,629 bytes) | Route target for "mobile/ios/android/background/checkpoint" |
| `references/refactoring-to-prompt-native.md` | Routing table, Reference Files list | Yes (8,560 bytes) | Route target for "review/refactor/existing" |

**Summary:** 14 internal file references. All 14 exist. No broken references. No external file references. No references outside the skill directory.

---

## 6. Skill Cross-References

**None.** SKILL.md contains no explicit references to other skills in the plugin or across plugins. There are no `skills/` path references, no `@skill` directives, and no named cross-skill dependencies.

---

## 7. Agent References

**None.** SKILL.md contains no references to agents by path or name. No `agents/` paths, no `@agent` directives, no subagent invocation patterns.

---

## 8. Other Markdown File Analysis

All 14 reference files are non-SKILL.md markdown. Sizes are from GitHub API. Word counts and token estimates are derived from fetched content length and structure.

| File | Size (bytes) | Est. lines | Est. words | Est. tokens | Description | Referenced in SKILL.md |
|------|-------------|-----------|-----------|-------------|-------------|------------------------|
| action-parity-discipline.md | 11,128 | ~210 | ~1,700 | ~2,267 | Capability mapping workflow, parity audit procedures, system prompt documentation patterns for tools | Routing table + Reference Files list |
| agent-execution-patterns.md | 13,317 | ~250 | ~2,050 | ~2,733 | Completion signals (complete_task tool), partial completion/resume, model tier selection, context management for long sessions | Routing table + Reference Files list |
| agent-native-testing.md | 16,749 | ~315 | ~2,575 | ~3,433 | Outcome-based testing framework, AgentTestHarness class, parity test automation, CI/CD integration with token cost awareness | Routing table + Reference Files list |
| architecture-patterns.md | 17,241 | ~325 | ~2,650 | ~3,533 | Event-driven architecture, two-layer git strategy, multi-instance branching, unified orchestrator, approval gates, model tier selection | Routing table + Reference Files list |
| dynamic-context-injection.md | 9,612 | ~180 | ~1,480 | ~1,973 | Runtime context injection patterns (Swift, TypeScript, template-based), available resources/state/capabilities structure | Routing table + Reference Files list |
| files-universal-interface.md | 10,092 | ~190 | ~1,550 | ~2,067 | File-as-interface rationale, entity-scoped directory organization, context.md pattern, conflict resolution strategies | Routing table + Reference Files list |
| from-primitives-to-domain-tools.md | 11,788 | ~220 | ~1,815 | ~2,420 | Progressive tool architecture, three scenarios for domain tool justification, code graduation criteria, CRUD completeness | Routing table + Reference Files list |
| mcp-tool-design.md | 15,658 | ~295 | ~2,410 | ~3,213 | MCP tool design principles, dynamic capability discovery vs static mapping, CRUD completeness, descriptive naming, rich outputs | Routing table + Reference Files list |
| mobile-patterns.md | 25,629 | ~480 | ~3,940 | ~5,253 | iOS storage (iCloud Documents), checkpoint/resume state machine, permission handling, cost-aware model selection, offline graceful degradation, battery awareness | Routing table + Reference Files list |
| product-implications.md | 12,976 | ~245 | ~1,995 | ~2,660 | Progressive disclosure design, latent demand discovery via usage logging, approval framework matrix (stakes x reversibility), transparency patterns | Routing table + Reference Files list |
| refactoring-to-prompt-native.md | 8,560 | ~160 | ~1,315 | ~1,753 | Six-step refactoring strategy, red-flag identification, when code still belongs in code vs prompts | Routing table + Reference Files list |
| self-modification.md | 7,866 | ~148 | ~1,210 | ~1,613 | Approval workflows for code changes, build verification with rollback, health monitoring, git-based architecture, when to use vs avoid | Routing table + Reference Files list |
| shared-workspace-architecture.md | 20,874 | ~393 | ~3,210 | ~4,280 | Unified filesystem design, directory structure (entity-scoped), essential file tool primitives, collaboration patterns (draft/refine, seed/expand, append-only), security boundaries, iOS iCloud sync | Routing table + Reference Files list |
| system-prompt-design.md | 6,522 | ~123 | ~1,005 | ~1,340 | Features-as-prompt-sections pattern, judgment criteria over rules, system prompt structure template, iteration approach | Routing table + Reference Files list |

**Total reference corpus:** ~190,012 bytes, ~3,533 estimated lines, ~27,705 estimated words, ~36,940 estimated tokens.

---

## 9. Structural Observations

### YAML Frontmatter Fields

Two fields present:

```yaml
name: agent-native-architecture
description: Build applications where agents are first-class citizens. Use this skill when designing autonomous agents, creating MCP tools, implementing self-modifying systems, or building apps where features are outcomes achieved by agents operating in a loop.
```

- `name`: slug-format skill identifier
- `description`: invocation trigger description (247 characters). Includes explicit "use this skill when" language covering four distinct invocation scenarios.
- No `version`, `author`, `tags`, or `tools` fields present.

### Code Blocks

**Count:** 6 code blocks in SKILL.md

**Languages used:**

| Language | Count | Purpose |
|----------|-------|---------|
| (unlabeled / plain) | 2 | Pseudo-code tool comparison (Granularity section) |
| markdown/text | 1 | System prompt example (Quick Start Step 2) |
| typescript | 2 | Tool array definition (Quick Start Step 1), agent.run() call (Quick Start Step 3) |
| sql-like table | 0 | Tables use markdown pipe syntax, not fenced blocks |

**Reference files collectively contain many additional TypeScript, Swift, and pseudocode blocks** (exact counts not available from WebFetch summaries, but confirmed present in: agent-native-testing.md, architecture-patterns.md, dynamic-context-injection.md, mobile-patterns.md, shared-workspace-architecture.md, mcp-tool-design.md).

### Lists vs Prose Ratio

SKILL.md is approximately 45% prose, 35% lists/tables/checklists, 20% code blocks by visual weight.

Structured elements:
- 2 markdown tables (capability map in Parity section; routing dispatch table)
- 1 numbered interactive menu (13 items, "What Aspect..." section)
- 7 checklist sections within Architecture Review Checklist (25+ checkbox items total)
- 3 numbered Quick Start steps
- 1 bulleted Reference Files section (14 items, two sub-groups)
- 5 checklist sections in Success Criteria (25+ checkbox items total)
- 1 numbered flywheel list (Emergent Capability section)
- Multiple bullet lists within Anti-Patterns section

### Conditional Logic

The Routing section is the primary conditional structure: a dispatch table mapping user response strings to specific reference file reads. This is not executable logic but a directive to the agent: "if user says X, read file Y." The "Wait for response before proceeding" instruction before the routing table enforces a blocking interaction gate.

The Architecture Review Checklist and Success Criteria sections contain conditional applicability: sections marked "(if applicable)" for Mobile patterns, scoping mobile-specific checks only when relevant.

### Templates

- **Capability Map template** (H3 "1. Parity"): A 4-row markdown table showing the pattern of mapping UI actions to agent tool equivalents. Reusable as a documentation artifact.
- **Quick Start template** (H2 "Quick Start"): Three-step scaffold (define tools / write system prompt / run loop) with TypeScript stubs. Directly copy-paste usable.
- **Architecture Review Checklist**: Functions as a fill-in verification template for new system designs.
- **Success Criteria checklists**: Functions as a self-assessment template.

### Examples

- **Granularity section**: Side-by-side "Less granular" vs "More granular" tool design comparison with annotated pseudocode.
- **Composability section**: "Weekly review" feature implemented as a prose prompt example.
- **Emergent Capability section**: Cross-reference meeting notes with tasks example (open-ended request the agent can handle without explicit feature).
- **Improvement Over Time**: Three-level prompt refinement hierarchy (developer/user/agent).
- **Anti-Patterns section**: Named anti-patterns with wrong/right code comparisons (process_feedback, static HealthKit tool mapping, incomplete CRUD).
- **Context starvation anti-pattern**: Concrete dialogue example showing agent failure mode.

### Constraints Sections

Constraints are embedded within principle sections rather than in a dedicated "Constraints" heading:
- "The discipline:" callouts after each principle (Parity, Granularity, Composability, Emergent Capability) state the behavioral constraint in imperative form.
- "The test:" callouts at the end of each principle provide a binary pass/fail verification.
- Anti-Patterns section is effectively a constraints list (what not to do), with "THE CARDINAL SIN" labeling the most severe constraint.
- Architecture Review Checklist enforces constraints pre-implementation.
- Success Criteria enforces constraints post-implementation.

### Interactive Routing Pattern

SKILL.md implements a deliberate two-phase interaction pattern:
1. Present 13-item numbered menu, explicitly instructing the agent to wait for user response.
2. Use routing table to dispatch to the appropriate reference file, then apply patterns to user's context.

This is a progressive disclosure mechanism: the skill does not dump all 190KB of reference content into context, but gates access behind user intent declaration. Only the relevant reference file is loaded per interaction.
