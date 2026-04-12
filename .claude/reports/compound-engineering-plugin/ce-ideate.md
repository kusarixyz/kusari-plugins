---
repository: EveryInc/compound-engineering-plugin
branch: main
skill-path: plugins/compound-engineering/skills/ce-ideate
analyzed: 2026-04-11
---

# Skill Analysis: ce:ideate

## 1. Overview

**Skill name:** ce:ideate
**Title text:** `Generate Improvement Ideas` (26 chars)
**Description:** `Generate and critically evaluate grounded improvement ideas for the current project. Use when asking what to improve, requesting idea generation, exploring surprising improvements, or wanting the AI to proactively suggest strong project directions before brainstorming one in depth. Triggers on phrases like 'what should I improve', 'give me ideas', 'ideate on this project', 'surprise me with improvements', 'what would you change', or any request for AI-generated project improvement suggestions rather than refining the user's own idea.` (543 chars)

**Total files (recursive):** 2
**Subdirectories:** 1 (`references/`)

**File list:**
| File | Size (bytes) |
|------|-------------|
| `SKILL.md` | 10122 |
| `references/post-ideation-workflow.md` | 5173 |

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Line count | 156 |
| Word count | 1,475 |
| Character count | 10,122 |
| Estimated token count (words / 0.75) | 1,967 |

---

## 3. Document Structure Depth

### SKILL.md headings (in order)

| Line | Level | Heading |
|------|-------|---------|
| 7 | H1 | Generate Improvement Ideas |
| 19 | H2 | Interaction Method |
| 25 | H2 | Focus Hint |
| 38 | H2 | Core Principles |
| 44 | H2 | Execution Flow |
| 46 | H3 | Phase 0: Resume and Scope |
| 48 | H4 | 0.1 Check for Recent Ideation Work |
| 68 | H4 | 0.2 Interpret Focus and Volume |
| 94 | H3 | Phase 1: Codebase Scan |
| 134 | H3 | Phase 2: Divergent Ideation |

**Max depth:** H4 (4 levels)
**Count per level:**
- H1: 1
- H2: 4
- H3: 3
- H4: 2

**Total headings:** 10

---

## 4. Content Specificity Assessment

**Score: 4 / 5**

The skill is highly specific and operational. Instructions reference exact agent names, conditional routing logic, volume defaults with numeric thresholds, and precise file paths. Abstraction is present only in framing (e.g., "ideation frames"), not in execution steps.

**Justifications:**

1. Dispatch instructions are concrete to named agents and model tiers:
   > "dispatch `compound-engineering:research:learnings-researcher` with a brief summary of the ideation focus"
   > "dispatch a general-purpose sub-agent using the platform's cheapest capable model (e.g., `model: \"haiku\"` in Claude Code)"

2. Volume defaults are numerically bounded with explicit override semantics:
   > "each ideation sub-agent generates about 8-10 ideas (yielding ~30 raw ideas across agents, ~20-25 after dedupe)" / "keep the top 5-7 survivors"

3. The lazy-load constraint on the reference file is precisely conditional:
   > "read `references/post-ideation-workflow.md` for the adversarial filtering rubric ... Do not load this file before Phase 2 agent dispatch completes."

The score is 4 rather than 5 because Phase 2 frame definitions are somewhat abstract ("user/operator pain and friction", "assumption-breaking or reframing") and leave judgment to the model.

---

## 5. Internal File References

| Line | Reference | Purpose |
|------|-----------|---------|
| 17 | `docs/ideation/` | Output artifact directory |
| 50 | `docs/ideation/` | Resume check location |
| 102 | `AGENTS.md`, `CLAUDE.md`, `README.md` | Project documentation to scan in Phase 1 quick context sub-agent prompt |
| 156 | `references/post-ideation-workflow.md` | Lazy-loaded reference for Phases 3-6; explicitly deferred until Phase 2 completes |

---

## 6. Skill Cross-References

| Skill | How Referenced |
|-------|---------------|
| `ce:brainstorm` | Named 4 times as the downstream consumer of ideation output; routing to it is an explicit constraint ("Do not skip to planning from ideation output") |
| `ce:plan` | Mentioned once in the workflow positioning table (line 15); not invoked directly |
| `compound-engineering:research:learnings-researcher` | Dispatched in Phase 1 (line 112) |
| `compound-engineering:research:issue-intelligence-analyst` | Conditionally dispatched in Phase 1 (line 114) |
| `compound-engineering:research:slack-researcher` | Conditionally dispatched in Phase 1, opt-in only (line 128) |

---

## 7. Agent References

| Agent / Tool | Context |
|-------------|---------|
| `AskUserQuestion` | Named as blocking question tool for Claude Code platform |
| `request_user_input` | Named as blocking question tool for Codex platform |
| `ask_user` | Named as blocking question tool for Gemini platform |
| `Glob` | Referenced in inline sub-agent prompt for directory discovery |
| Anonymous quick-context sub-agent | Dispatched in Phase 1 with a cheapest-model directive (e.g., `model: "haiku"`); no named skill |

No direct references to agents defined within the ce-ideate skill directory itself. All agent dispatches are either named skills (see Section 6) or an anonymous sub-agent with an inline prompt.

---

## 8. Other Markdown File Analysis: `references/post-ideation-workflow.md`

| Metric | Value |
|--------|-------|
| Line count | 166 |
| Word count | 823 |
| Character count | 5,173 |
| Estimated token count (words / 0.75) | 1,097 |

### Headings

| Line | Level | Heading |
|------|-------|---------|
| 1 | H1 | Post-Ideation Workflow |
| 5 | H2 | Phase 3: Adversarial Filtering |
| 29 | H2 | Phase 4: Present the Survivors |
| 53 | H2 | Phase 5: Write the Ideation Artifact |
| 79 | H1 | Ideation: \<Title\> (template heading inside fenced block) |
| 81 | H2 | Codebase Context (template) |
| 84 | H2 | Ranked Ideas (template) |
| 86 | H3 | 1. \<Idea Title\> (template) |
| 94 | H2 | Rejection Summary (template) |
| 100 | H2 | Session Log (template) |
| 109 | H2 | Phase 6: Refine or Hand Off |
| 119 | H3 | 6.1 Brainstorm a Selected Idea |
| 129 | H3 | 6.2 Refine the Ideation |
| 141 | H3 | 6.3 Share to Proof |
| 147 | H3 | 6.4 End the Session |
| 155 | H2 | Quality Bar |

Note: lines 79-103 appear inside a fenced markdown code block (the artifact template). Those headings are not structural headings of the document itself.

**Max depth (document):** H3
**Structural heading count:** H1: 1, H2: 6 (Phase 3, 4, 5, 6, Quality Bar, plus one in the template block), H3: 5

**Skill/agent cross-references in this file:**
- `ce:brainstorm` referenced in Phase 6.1 (invoke as handoff)
- "Proof" (sharing target) referenced in Phase 6.3 and Phase 6.4

**Code blocks:** 1 fenced block (lines ~57-103), containing the full ideation artifact markdown template with YAML frontmatter, all section headers, and a rejection summary table skeleton.

---

## 9. Structural Observations

### YAML Frontmatter (SKILL.md)

Present. Fields:
- `name: ce:ideate`
- `description`: 543-char natural-language trigger description including example trigger phrases
- `argument-hint: "[feature, focus area, or constraint]"`

No `tools`, `model`, or `mode` keys. Model and mode selection delegated to inline dispatch logic within the document.

### Code Blocks

**SKILL.md:** Zero fenced code blocks. Inline code spans are used extensively for tool names, file paths, argument examples, and agent/skill identifiers.

**post-ideation-workflow.md:** One fenced code block spanning ~47 lines, containing the full ideation artifact template (YAML frontmatter + markdown structure). This is the only template content in the skill.

### Lists vs. Prose

The skill is list-heavy. Roughly 60% of the body content uses ordered or unordered lists. Prose paragraphs appear primarily in Phase 1 (sub-agent prompt text) and the Slack context conditional block. Phase 2 and Phase 3 are almost entirely bulleted. The Core Principles section uses a numbered list with bolded lead terms.

### Conditional Logic

Substantial conditional routing is present and explicit:
- Resume vs. fresh start (Phase 0.1): topic/path/recency matching with 4 conditions
- Issue-tracker intent detection (Phase 0.2): positive triggers vs. negative triggers explicitly enumerated
- Slack dispatch: 3-branch conditional (tools+asked / tools+not-asked / no-tools+asked)
- Issue intelligence failure handling: error logging + graceful fallback
- Frame selection (Phase 2): issue-cluster-derived frames vs. 4 default frames
- Lazy file load: `references/post-ideation-workflow.md` deferred until Phase 2 completes

### Templates

One artifact template (in `references/post-ideation-workflow.md`, fenced block): complete markdown document structure with YAML frontmatter, all required sections, and a rejection summary table. Fields marked with `[...]` notation for fill-in. Session log uses a dated bullet format.

### Examples

Inline examples throughout:
- Argument examples: `DX improvements`, `plugins/compound-engineering/skills/`, `low-complexity quick wins`, `top 3`, `100 ideas`
- Volume override examples: `top 3`, `100 ideas`, `go deep`, `raise the bar`
- Issue-tracker trigger examples: `bugs`, `github issues`, `open issues`
- Non-trigger examples (focus hints only): `bug in auth`, `fix the login issue`, `the signup bug`
- Platform tool name examples: `AskUserQuestion`, `request_user_input`, `ask_user`
- Model tier example: `model: "haiku"`
- Glob pattern examples: `*`, `*/*`

### Constraints

Explicit prohibitions:
- "Do not generate abstract product advice detached from the repository"
- "Do not skip to planning from ideation output"
- "Do not dispatch sub-agents for critique" (Phase 3)
- "Do not generate replacement ideas in this phase unless explicitly refining" (Phase 3)
- "Do not load this file before Phase 2 agent dispatch completes"
- Do not auto-dispatch Slack (opt-in only)
- Do not create a branch or push at session end
- Do not tier down model for Phase 2 ideation sub-agents

### Deferred Loading Pattern

The most structurally notable pattern: Phases 3-6 are entirely offloaded to `references/post-ideation-workflow.md`, which is explicitly deferred until Phase 2 sub-agents complete. This keeps the main SKILL.md focused on the front half of the workflow and avoids front-loading the full reference into context. The instruction to read it appears on the last line of SKILL.md (line 156).

### Combined Token Budget

Total across both files: 1,975 + 1,097 = 3,072 estimated tokens (at words/0.75). If both files are loaded simultaneously, they constitute a non-trivial context contribution but remain well under typical limits.
