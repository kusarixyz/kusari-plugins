---
name: create-skill
description: Guide the creation of well-structured Claude Code plugin skills. Use when the user wants to create a new skill, design a skill from scratch, write a SKILL.md, or asks how to structure a skill for a plugin. Also use when the user describes a capability or workflow they want to encode as a skill and needs help with structure, specificity, file organization, or best practices.
---

When this skill is loaded, output exactly this block before any other response:

```
░█░█░█░█░█▀▀░█▀█░█▀▄░▀█▀░░░░░█▀▀░█░█░▀█▀░█░░░█░░░█▀▀
░█▀▄░█░█░▀▀█░█▀█░█▀▄░░█░░▄▄▄░▀▀█░█▀▄░░█░░█░░░█░░░▀▀█
░▀░▀░▀▀▀░▀▀▀░▀░▀░▀░▀░▀▀▀░░░░░▀▀▀░▀░▀░▀▀▀░▀▀▀░▀▀▀░▀▀▀
```

# Create Skill

Build a well-structured Claude Code plugin skill through guided co-design.

## Core Principles

1. **Classify, don't ask taxonomy.** Determine the skill type from what the user describes. Never ask "is this a capability or process skill?" -- infer it, explain the classification in one line, and let the user correct if needed.
2. **Structure follows intent.** The file organization, heading depth, and content patterns are downstream of the skill type. Do not ask structural questions. Infer them.
3. **Specificity is calibrated, not maximized.** A domain-knowledge skill needs code examples. A workflow skill needs prose directives. Both need explicit constraints. Neither needs the other's patterns forced onto it.
4. **Every reference must resolve.** No file path in SKILL.md may point to a file that does not exist. Verify before finalizing.
5. **Context cost is real.** Every token in SKILL.md is loaded into context on every invocation. Justify the cost of every section. Split to references/ when content is conditionally needed.

## Phase 0: Understand the Intent

Read `$ARGUMENTS` if provided. If the user gave a description of what they want, use it. If not, ask one question:

> What should this skill help with? Describe the task, domain, or workflow it should cover.

From the user's response, extract:
- **Domain** -- what subject or task area does this cover?
- **Trigger conditions** -- when should this skill activate?
- **Output** -- what does the skill produce? (files, plans, code, decisions, knowledge)
- **Duration** -- single-turn task or multi-phase workflow?
- **Agent needs** -- does this require parallel research, review, or orchestration?

## Phase 1: Classify and Confirm

### 1.1 Determine Skill Type

Classify the skill into one of three types based on the extracted intent:

**Capability skill** -- teaches the model a domain it does not already know. The user brings the task; the skill brings the knowledge. The model decides how to apply the knowledge based on the user's specific request.

Signals: the skill is about a file format, API, library, framework, creative medium, or technical domain. The output is a generated artifact (file, code, document). The task completes in a single model turn. No sub-agent coordination needed.

Examples from analysis: docx, pdf, xlsx, pptx, claude-api, algorithmic-art, andrew-kane-gem-writer.

**Process skill** -- defines a multi-step workflow the model follows. The user brings the problem; the skill brings the procedure. The model's judgment is constrained to documented decision points within each phase.

Signals: the task spans multiple phases with intermediate outputs. The skill needs conditional branching, agent dispatch, or user interaction gates. The output is a decision, plan, diagnosis, or knowledge capture. Wrong output is subtle (missed root cause, incomplete plan) rather than visually obvious.

Examples from analysis: ce-debug, ce-plan, ce-brainstorm, ce-compound, ce-compound-refresh, ce-ideate.

**Hybrid skill** -- combines domain knowledge with a structured workflow. Part of the skill is reference material; part is a phased procedure.

Signals: the skill teaches a domain AND defines how to apply it step by step. The reference sections are consulted during specific workflow phases.

Examples from analysis: skill-creator (teaches skill writing + defines create-eval-improve workflow), mcp-builder (teaches MCP protocol + defines 4-phase build process).

### 1.2 Present Classification

Present the classification to the user in one sentence:

> This is a [type] skill -- [one-line explanation of why]. [One-line implication for structure.]

Examples:
- "This is a capability skill -- it teaches the model how to work with GraphQL schemas. The structure will be a flat reference with code examples organized by task type."
- "This is a process skill -- it defines a debugging workflow with investigation, diagnosis, and fix phases. The structure will use numbered phases with conditional gates."
- "This is a hybrid skill -- it teaches Terraform patterns AND defines a plan-apply-verify workflow. Reference sections will feed into specific workflow phases."

Wait for the user to confirm or correct before proceeding.

### 1.3 Determine Structural Parameters

Based on the confirmed type, set these parameters silently (do not present them as choices):

**Capability skill defaults:**
- Document structure: flat H2/H3, random-access sections
- Primary content: code blocks with WRONG/CORRECT pairs, API references, examples
- Heading depth: H3 max (H4 only for deeply nested reference subsections)
- File split threshold: >3,000 tokens in SKILL.md triggers split to references/
- Agent integration: none unless the skill involves evaluation or review
- Coupling: standalone (zero cross-skill references)

**Process skill defaults:**
- Document structure: numbered phases (Phase 0, 1, 2, ...)
- Primary content: prose directives, decision tables, output templates, agent dispatch specs
- Heading depth: H4 typical (phases > sub-phases > steps)
- File split threshold: >2,000 tokens OR conditionally-needed content triggers split to references/
- Agent integration: likely -- plan for research and review dispatch points
- Coupling: determined by whether this skill fits into a larger workflow
- Phase 0: always include resume detection and routing/triage
- Constraints: repeat at decision points where drift is likely

**Hybrid skill defaults:**
- Document structure: reference sections (flat H2/H3) followed by workflow section (phased)
- Primary content: code blocks in reference sections, prose directives in workflow sections
- Heading depth: H3 for reference, H4 for workflow
- File split: reference material in references/, workflow in SKILL.md
- Agent integration: conditional per workflow phase

## Phase 2: Design the Skill

### 2.1 Frontmatter

Draft the YAML frontmatter. Required fields:

```yaml
---
name: <skill-name>
description: <trigger description>
---
```

**Name:** lowercase kebab-case or colon-namespaced (`ce:plan`, `create-skill`). Match the directory name.

**Description:** This is the primary trigger surface. Quality rules:
- Start with what the skill does, not what it is
- Include 3-5 explicit trigger phrases ("Use when the user says...")
- For complex skills, include negative triggers ("Do NOT use when...")
- Length guidance: 200-400 chars for focused skills, 400-700 chars for broad skills
- Longer descriptions correlate with more precise routing -- do not compress for brevity

**Optional fields** (add only when needed):
- `argument-hint: "[what to pass]"` -- when the skill accepts arguments
- `disable-model-invocation: true` -- when the skill performs destructive operations or is orchestration-only

### 2.2 Section Design

Based on the skill type and the user's described requirements, design the section outline.

**For capability skills**, organize by task type. Read `references/capability-patterns.md` for the structural template and conventions.

**For process skills**, organize by phase. Read `references/process-patterns.md` for the structural template and conventions.

**For hybrid skills**, combine both: reference sections first (flat), then workflow section (phased). Apply the relevant patterns from both reference files.

Present the proposed section outline to the user. One level of headings only -- do not expand sub-sections yet. Ask if the coverage matches their intent.

### 2.3 Specificity Calibration

For each major section in the outline, determine the right specificity approach:

| Content type | Best expressed as | Example |
|---|---|---|
| API usage, library calls, CLI commands | Fenced code blocks with language tags | `python scripts/recalc.py output.xlsx` |
| Correct vs. incorrect patterns | Side-by-side WRONG/CORRECT code pairs | Unicode bullets (wrong) vs numbering config (correct) |
| Decision logic | Markdown tables with conditions and actions | Overlap level -> keep / update / create new |
| Sequential procedures | Numbered prose directives | "1. Run the test suite. 2. If failures..." |
| Constraints and prohibitions | Bold inline rules with rationale | "NEVER use `data_only=True` -- this destroys formulas on save" |
| Output format | Fenced template blocks with placeholders | Debug summary template with named fields |
| Conditional behavior | Bold-labeled branches or decision tables | "**Lightweight:** skip Phase 3. **Standard:** run Phase 3." |

### 2.4 Context Budget

Estimate the token cost of the proposed outline. Rules:
- SKILL.md target: under 3,000 tokens for capability skills, under 6,000 for process skills
- If the estimate exceeds the target, identify sections that are conditionally needed and move them to references/
- Each reference file must have a clear load condition ("Read this file when X")
- For process skills, enforce lazy-loading: "Do not load this file before Phase N completes"
- For capability skills, use implicit loading: "For advanced features, see references/advanced.md"

## Phase 3: Write the Content

Work through the outline section by section with the user. For each section:

1. Write the content following the specificity calibration from Phase 2
2. Apply constraint design rules from `references/constraint-patterns.md`
3. Verify every file path reference points to a file that exists (or will be created)
4. For process skills: check that each phase has a clear entry condition, exit condition, and handoff

### 3.1 Constraint Design

Constraints are the most important content in any skill. Rules for writing them:

- State constraints where they matter, not only at the top
- For process skills: repeat critical constraints at the decision points where drift is most likely. This is deliberate, not redundant.
- Use absolute language: "NEVER", "ALWAYS", "Do not" -- not "try to avoid", "prefer not to"
- Pair every constraint with its rationale -- a constraint without a reason gets ignored under pressure
- For code-domain constraints: embed in code comments at the point of use (`# CRITICAL: never require Rails directly`)
- For behavioral constraints: state as prose directives with the consequence of violation

### 3.2 Cross-Reference Design

**Standalone skills:** No cross-references. Every capability the skill needs must be self-contained or delegated to scripts.

**Pipeline skills:** Define explicit handoff points with conditions:
- Name the target skill by its invocation syntax (`/ce:brainstorm`, `document-review`)
- State the condition that triggers the handoff
- State what data passes to the next skill
- Make handoffs user-choice, not automatic (unless the skill is designed for autonomous pipelines)

## Phase 4: Write the Files

### 4.1 Create the directory structure

```
<skill-name>/
  SKILL.md
  references/          (if split content exists)
    <topic>.md
  scripts/             (if deterministic automation exists)
    <script>.py
  assets/              (if templates or binary assets exist)
    <template>.md
```

### 4.2 Write SKILL.md

Write the complete SKILL.md incorporating all content from Phase 3.

### 4.3 Write reference files

For each reference file identified in Phase 2.4, write the content. Each reference file:
- Has no YAML frontmatter (frontmatter is only for SKILL.md)
- Opens with an H1 title
- Is self-contained enough to be useful when loaded mid-workflow
- Does not duplicate content from SKILL.md -- it extends or specifies

### 4.4 Final Verification

Before presenting the result:
- Verify every file path in SKILL.md resolves to a file in the skill directory
- Verify SKILL.md token count is within the budget from Phase 2.4
- Verify the description field contains sufficient trigger phrases
- For process skills: verify every phase has entry/exit conditions
- For capability skills: verify every major section has at least one code example or concrete reference
- Read the SKILL.md from top to bottom as if encountering it for the first time -- does the structure make sense without prior context?

Present the complete file listing and ask the user to review.
