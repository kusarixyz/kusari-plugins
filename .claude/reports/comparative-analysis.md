# Comparative Analysis: Two Approaches to Skill Design

**Subjects:**
- **Anthropic Skills** (anthropics/skills) -- 17 skills analyzed
- **Compound Engineering** (EveryInc/compound-engineering-plugin) -- 10 of 40 skills analyzed

**Date:** 2026-04-11

---

## 1. Fundamental Design Philosophy

These two repositories represent opposing ends of a design spectrum. The difference is not incremental -- it is architectural.

**Anthropic Skills treats the model as a craftsman.** Skills provide domain knowledge, tool references, and quality standards. The model decides how to apply them. There is no prescribed execution order. The skill says "here is everything you need to know about DOCX files" and trusts the model to navigate the reference material based on the user's request.

**Compound Engineering treats the model as an executor.** Skills define deterministic workflows with numbered phases, conditional gates, and explicit dispatch instructions. The model follows a state machine. The skill says "at Phase 1, launch these three agents in parallel; at Phase 2, wait for all to complete; at Phase 3, present findings using this exact template."

Neither approach is wrong. They solve different problems. Anthropic Skills optimizes for breadth of coverage across many unrelated domains. Compound Engineering optimizes for depth of orchestration within a single team's development workflow.

---

## 2. Structural Comparison

### 2.1 Document Organization

| Dimension | Anthropic Skills | Compound Engineering |
|-----------|-----------------|---------------------|
| Primary structure | Flat reference sections (H2/H3) | Numbered phase pipeline (Phase 0, 1, 2...) |
| Typical H2 sections | Overview, Quick Reference, Dependencies | Core Principles, Execution Flow, Phase N |
| Heading depth mode | H3 (10/17) | H4 (5/10) |
| Document reads like | A reference manual or cookbook | A procedure manual or runbook |
| Entry point | Any section (random access) | Phase 0 (sequential access) |

Anthropic Skills are designed for random access. A model working on a PDF task can jump directly to the "Merge PDFs" subsection without reading anything else. The flat H2/H3 structure supports this -- each section is self-contained.

Compound Engineering skills are designed for sequential execution. Phase 0 must complete before Phase 1 begins. Skipping ahead is explicitly prohibited in most skills. The deep H4/H5 hierarchy reflects nested decision trees within each phase.

### 2.2 Size and Density

| Metric | Anthropic (median) | Compound (median) | Ratio |
|--------|--------------------|--------------------|-------|
| SKILL.md tokens | 1,720 | 2,585 | 1.5x |
| SKILL.md max tokens | 6,293 | 9,873 | 1.6x |
| Total headings | 17 | 28.5 | 1.7x |
| Explicit prohibitions | ~5 | ~6-7 | 1.3x |

Compound Engineering skills are consistently larger, but the size difference is modest (1.5x median). The real difference is in what fills that space: Anthropic skills fill it with code blocks and API references; Compound Engineering fills it with conditional logic, agent dispatch specs, and output templates.

### 2.3 Code vs. Prose Ratio

Anthropic Skills are code-block-heavy. The median skill contains 5-10 fenced code blocks with executable examples (Python, JavaScript, bash, XML). Some skills (docx, pptx, xlsx) are >50% code by line count. The code is the instruction -- the model learns what to do by seeing working examples.

Compound Engineering skills contain far fewer code blocks. Most code blocks are output templates or invocation syntax, not executable examples. ce-ideate has zero code blocks. The instruction is prose-based -- explicit imperative directives telling the model what to do at each step.

This maps directly to the craftsman vs. executor distinction. A craftsman learns from examples. An executor follows written procedures.

---

## 3. Coupling and Composition

### 3.1 Inter-Skill Dependencies

| Pattern | Anthropic Skills | Compound Engineering |
|---------|-----------------|---------------------|
| Cross-skill references | 0/17 (0%) | 8/10 (80%) |
| Skills form a graph | No -- every skill is an island | Yes -- directed workflow graph |
| Shared infrastructure | scripts/office/ duplicated 3x | Named agent namespaces shared across skills |
| Portability | Any skill works standalone | Most skills assume the presence of others |

Anthropic Skills achieves zero coupling at the cost of duplication. Three skills (docx, pptx, xlsx) share an identical `scripts/office/` directory with 40+ files copied into each. This is a deliberate trade: portability over DRY.

Compound Engineering achieves tight orchestration at the cost of portability. ce-ideate depends on ce-brainstorm as its downstream consumer. ce-debug offers handoffs to ce-compound and ce-brainstorm. Removing one skill degrades the functionality of others.

### 3.2 The Workflow Graph

Compound Engineering's skills form an explicit pipeline:

```
ce-ideate -> ce-brainstorm -> ce-plan -> ce-work
                                |
                                v
                           ce-compound -> ce-compound-refresh
                                |
                           ce-debug (re-enters at any point)
```

Each arrow is a documented handoff with explicit conditions. This graph does not exist in Anthropic Skills -- there are no handoffs, no pipelines, no upstream/downstream relationships.

### 3.3 Agent Integration

| Pattern | Anthropic Skills | Compound Engineering |
|---------|-----------------|---------------------|
| Skills referencing agents | 1/17 (6%) | 7/10 (70%) |
| Max agents per skill | 3 (skill-creator) | 14 (ce-plan) |
| Agent dispatch pattern | Read agent file, spawn | Namespaced identifiers with model tier |
| Agent role separation | Grader, comparator, analyzer | Research namespace + review namespace |

Anthropic Skills largely ignore agents. skill-creator is the sole exception, and even there the agents are tightly scoped evaluation tools.

Compound Engineering uses agents as first-class execution units. The `compound-engineering:research:*` and `compound-engineering:review:*` namespaces create a reusable agent library that skills compose from. ce-plan dispatches 6 agents during planning and up to 8 more during deepening. The agent surface area is an order of magnitude larger.

---

## 4. Context Window Management

Both repositories grapple with the same constraint -- limited context window -- but solve it differently.

### 4.1 Anthropic Skills: Progressive Disclosure via Architecture

Skills use three architectural patterns to manage context:

1. **Monolithic reference** (10/17): Everything in SKILL.md. Works because the skills are small enough (median 1,720 tokens).
2. **Router/dispatcher** (3/17): SKILL.md is thin, routes to sub-files by input type (pdf -> forms.md or reference.md).
3. **Progressive disclosure index** (4/17): SKILL.md is a compact index with Quick Reference sections. Full content loads from sub-files on demand (claude-api routes to 38+ language-specific files).

The loading is implicit. SKILL.md says "For advanced features, see REFERENCE.md" but does not enforce when that file gets read. The model decides.

### 4.2 Compound Engineering: Explicit Lazy-Loading with Constraints

Seven of ten skills enforce deferred loading as a stated rule:

> "Read `references/post-ideation-workflow.md` for the adversarial filtering rubric... Do not load this file before Phase 2 agent dispatch completes."

> "Read them on-demand at the step that needs them -- do not bulk-load at skill start."

This is not architectural suggestion. It is an explicit prohibition. The skill actively tells the model when it is forbidden to read a file. This level of context management is absent from Anthropic Skills entirely.

The compound approach is more aggressive but also more fragile -- it relies on the model obeying prose-based load constraints. If the model preloads a file anyway, the constraint fails silently.

---

## 5. Specificity and Trust

### 5.1 The Specificity Gap

| Score | Anthropic Skills | Compound Engineering |
|-------|-----------------|---------------------|
| 2/5 | 1 (6%) | 0 |
| 3/5 | 1 (6%) | 2 (20%) |
| 4/5 | 10 (59%) | 1 (10%) |
| 5/5 | 5 (29%) | 7 (70%) |

The distributions barely overlap. Anthropic Skills clusters at 4/5. Compound Engineering clusters at 5/5.

Score 4 means "mostly specific, actionable instructions with some framing." Score 5 means "extremely granular, step-by-step instructions with exact patterns/templates."

The difference is a design choice about trust. Anthropic Skills trusts the model to make judgment calls within a domain. It provides the knowledge; the model applies it. Compound Engineering does not trust the model with execution decisions. It prescribes exactly what to do, when, and in what order. Judgment is constrained to narrow, documented decision points.

### 5.2 How Constraints Are Expressed

Anthropic Skills embeds constraints in code comments and section labels:

```ruby
# WRONG
require "active_record"
# CORRECT
ActiveSupport.on_load(:active_record) { ... }
```

```
### Lists (NEVER use unicode bullets)
```

Compound Engineering embeds constraints in prose directives, often repeated at multiple decision points:

> "Do not propose a fix until the full causal chain is explained." (stated twice in ce-debug)

> "Core principles are repeated at decision points because they matter most when the pressure to skip them is highest."

ce-debug explicitly acknowledges that constraints are repeated as an anti-drift mechanism. This is a design pattern for LLM behavior management that has no analog in Anthropic Skills.

### 5.3 Multi-Platform Targeting

Compound Engineering embeds cross-platform compatibility directly into skill text. Seven of ten skills name platform-specific tool variants:

> `AskUserQuestion` (Claude Code), `request_user_input` (Codex), `ask_user` (Gemini)

Anthropic Skills does not reference platform-specific tools. The skills assume Claude Code as the sole execution environment and do not account for alternative harnesses.

---

## 6. Content Type and Domain

### 6.1 What They Teach vs. What They Do

Anthropic Skills are predominantly domain-knowledge modules. They answer the question: "How do I work with X?" where X is a file format (PDF, DOCX, PPTX, XLSX), a creative medium (algorithmic art, canvas design), or a technology (Claude API, MCP servers). The skill provides the knowledge; the model provides the workflow.

Compound Engineering skills are predominantly workflow modules. They answer the question: "What do I do next?" The skill provides the workflow; the model provides the execution within each step.

| Category | Anthropic Skills | Compound Engineering |
|----------|-----------------|---------------------|
| File format manipulation | 5 (docx, pdf, pptx, xlsx, docx) | 0 |
| Creative output | 4 (algorithmic-art, canvas-design, frontend-design, theme-factory) | 0 |
| API/SDK reference | 2 (claude-api, mcp-builder) | 0 |
| Development workflow | 1 (skill-creator) | 7 (brainstorm, plan, debug, compound, compound-refresh, ideate, demo-reel) |
| Architecture/patterns | 0 | 2 (agent-native-architecture, agent-native-audit) |
| Domain-specific code style | 0 | 1 (andrew-kane-gem-writer) |

The repositories occupy almost entirely non-overlapping domain spaces. Anthropic Skills dominates document/media generation. Compound Engineering dominates development process orchestration.

### 6.2 Output Artifacts

| Output type | Anthropic Skills | Compound Engineering |
|-------------|-----------------|---------------------|
| Generated files (DOCX, PDF, XLSX, HTML) | Primary output | Not applicable |
| Code (implementations, scripts) | Secondary (skill-creator evals) | Not applicable |
| Planning documents | Not applicable | Primary (docs/brainstorms/, docs/plans/) |
| Knowledge documentation | Not applicable | Primary (docs/solutions/) |
| Visual evidence (GIFs, screenshots) | Not applicable | Secondary (ce-demo-reel) |

Anthropic Skills produces artifacts for end users. Compound Engineering produces artifacts for the development team.

---

## 7. Frontmatter and Metadata

| Field | Anthropic Skills | Compound Engineering |
|-------|-----------------|---------------------|
| `name` | 16/17 | 10/10 |
| `description` | 16/17 | 10/10 |
| `license` | 16/17 | 0/10 |
| `argument-hint` | 0/17 | 6/10 |
| `disable-model-invocation` | 0/17 | 2/10 |
| Median description length | 318 chars | 396 chars |

Key differences:

- Anthropic Skills includes `license` in every skill. Compound Engineering omits it entirely -- the license lives at the plugin level, not the skill level.
- Compound Engineering uses `argument-hint` to guide invocation syntax. Anthropic Skills relies entirely on the description for trigger matching.
- `disable-model-invocation: true` is a safety mechanism for destructive skills (ce-compound-refresh deletes files). No Anthropic skill needs this because none perform destructive operations.

---

## 8. Automation Strategy

### 8.1 Scripts vs. Agents

| Mechanism | Anthropic Skills | Compound Engineering |
|-----------|-----------------|---------------------|
| Python scripts | 10/17 skills | 1/10 skills |
| Named agents | 1/17 skills | 7/10 skills |
| Binary assets | 3/17 skills | 0/10 skills |
| Shared script infrastructure | scripts/office/ (3 skills) | None |

Anthropic Skills offloads computation to Python scripts. PDF form filling, XLSX formula recalculation, PPTX thumbnail generation, Office XML validation -- all handled by scripts the model invokes via bash. The model orchestrates; the scripts compute.

Compound Engineering offloads cognition to sub-agents. Research, analysis, review, pattern recognition -- all handled by named agents the model dispatches via the Task tool. The model orchestrates; the agents think.

This is a fundamental architectural divergence. Scripts are deterministic -- they always produce the same output for the same input. Agents are probabilistic -- they reason about code, synthesize findings, and produce variable output. Anthropic Skills uses deterministic tools for deterministic tasks. Compound Engineering uses probabilistic tools for probabilistic tasks.

### 8.2 Subagent Orchestration Patterns

Compound Engineering has developed a sophisticated vocabulary for agent dispatch:

- **Parallel research agents** -- multiple agents scan different data sources simultaneously (ce-compound Phase 1, ce-plan Phase 1)
- **Sequential write agents** -- agents that modify files run one at a time to avoid context exhaustion (ce-compound-refresh replacement agents)
- **Read-only investigation agents** -- agents constrained to read operations that cannot edit, create, or delete (ce-compound-refresh investigation agents)
- **Conditional review agents** -- triggered by problem_type or detected technology stack (ce-compound Phase 3)
- **Model tier specification** -- explicit control over which model runs the agent (`model: "haiku"` for cheap scans, `model: "sonnet"` for mid-tier synthesis)
- **Opt-in user-gated agents** -- agents that only run if the user explicitly requests them (slack-researcher across multiple skills)

None of these patterns exist in Anthropic Skills because agents are not a structural element of that system.

---

## 9. Error Handling and Drift Prevention

### 9.1 Anthropic Skills: Trust the Model

Error handling is minimal and implicit. Skills provide WRONG/CORRECT code pairs and NEVER constraints, but do not define recovery procedures for when the model makes a mistake. The assumption is that sufficient knowledge prevents errors.

### 9.2 Compound Engineering: Assume Drift

Compound Engineering assumes the model will drift from instructions under pressure and designs explicit countermeasures:

1. **Principle repetition at decision points.** ce-debug restates core principles at Phase 2 and Phase 3 entry points and documents why: "They are repeated at decision points because they matter most when the pressure to skip them is highest."

2. **Smart escalation procedures.** When the model gets stuck (2-3 failed hypotheses in ce-debug, 3 failed fix attempts), a named escalation table maps observable patterns to prescribed next moves rather than leaving the model to improvise.

3. **Scope tiering gates.** Skills like ce-brainstorm, ce-plan, and ce-compound classify work into Lightweight/Standard/Deep tiers at Phase 0, then enforce different behaviors per tier throughout execution. This prevents the model from applying deep-plan procedures to a lightweight task.

4. **Resume detection.** Five skills check for prior work at Phase 0 before starting fresh, preventing duplicate effort when a session is interrupted and restarted.

5. **Explicit "do not skip" constraints.** ce-compound: "Do NOT pre-select a mode. Do NOT skip this prompt." ce-debug: "Do not propose a fix until the full causal chain is explained."

These patterns reflect a different operational maturity. Anthropic Skills is written for a model that gets things right on the first try. Compound Engineering is written for a model that might get it wrong and needs guardrails.

---

## 10. Strengths and Weaknesses

### Anthropic Skills

**Strengths:**
- Zero coupling means any skill can be adopted independently
- Code-heavy content provides unambiguous implementation guidance
- Script-based automation gives deterministic, repeatable results
- Binary asset bundling (fonts, PDFs, tarballs) enables fully offline operation
- Simple mental model: one skill = one domain = one directory

**Weaknesses:**
- Infrastructure duplication (scripts/office/ copied 3x)
- No workflow composition -- cannot chain skills together
- No agent integration -- cannot leverage parallel research or review
- No drift prevention mechanisms for long-running tasks
- Single-platform assumption (Claude Code only)
- No resume/continuation logic for interrupted sessions

### Compound Engineering

**Strengths:**
- Workflow composition via skill handoff graph
- Sophisticated agent orchestration with role separation and model tier control
- Explicit context window management via lazy-loading constraints
- Drift prevention through principle repetition and escalation procedures
- Multi-platform targeting (Claude Code, Codex, Gemini)
- Resume detection prevents duplicate work

**Weaknesses:**
- High coupling -- removing one skill can break the workflow
- Prose-heavy instructions depend on model compliance with natural language directives
- Lazy-loading constraints can fail silently if the model preloads
- Large SKILL.md files (up to 9,873 tokens) consume significant context upfront
- Very few scripts -- limited deterministic automation
- Non-integer phase numbering (1.5, 1.75) signals organic growth without refactoring

---

## 11. Synthesis

The two approaches are complementary, not competitive. They solve different problems at different layers:

**Anthropic Skills operates at the capability layer.** It answers: "Can the model work with PDFs? Can it generate PowerPoint presentations? Can it build MCP servers?" Each skill adds a capability the model did not previously have. The skills are tools in a toolbox.

**Compound Engineering operates at the process layer.** It answers: "How should the team ideate, plan, debug, and document?" Each skill defines a workflow the team follows. The skills are procedures in a runbook.

A complete system would use both: Anthropic-style skills for domain capabilities (file formats, APIs, creative tools) and Compound-style skills for development process orchestration (planning, debugging, knowledge capture). The two layers do not conflict because they occupy different abstraction levels and reference different types of content.

The key design decisions for building new skills:

| Decision | Choose Anthropic-style when | Choose Compound-style when |
|----------|---------------------------|---------------------------|
| Domain | The skill teaches how to use a tool or format | The skill defines a multi-step process |
| Output | The output is a generated artifact (file, code, document) | The output is a decision, plan, or knowledge capture |
| Duration | The task completes in a single model turn | The task spans multiple phases with intermediate outputs |
| Agents | No sub-agent coordination needed | Multiple specialized agents contribute to the result |
| Coupling | The skill must work standalone | The skill fits into a larger workflow pipeline |
| Error model | Wrong output is visually obvious (broken PDF, bad code) | Wrong output is subtle (missed root cause, incomplete plan) |
| Model trust | High -- domain knowledge prevents errors | Low -- explicit guardrails needed to prevent drift |
