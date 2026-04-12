---
skill: ce:brainstorm
repository: EveryInc/compound-engineering-plugin
branch: main
analyzed: 2026-04-11
---

# Skill Analysis: ce:brainstorm

## 1. Overview

**Skill name:** ce:brainstorm

**Title text:** `Brainstorm a Feature or Improvement` (38 characters)

**Description:** (from YAML frontmatter)
> Explore requirements and approaches through collaborative dialogue before writing a right-sized requirements document and planning implementation. Use for feature ideas, problem framing, when the user says 'let's brainstorm', or when they want to think through options before deciding what to build. Also use when a user describes a vague or ambitious feature request, asks 'what should we build', 'help me think through X', presents a problem with multiple valid solutions, or seems unsure about scope or direction — even if they don't explicitly ask to brainstorm.

Description character count: 560 characters

**Total files (recursive):** 5
**Subdirectories:** 1 (`references/`)

**File list:**
| File | Bytes |
|---|---|
| SKILL.md | 14192 |
| references/handoff.md | 4424 |
| references/requirements-capture.md | 5666 |
| references/universal-brainstorming.md | 4528 |
| references/visual-communication.md | 2881 |
| **Total** | **31691** |

---

## 2. SKILL.md Metrics

| Metric | Value |
|---|---|
| Byte size | 14192 |
| Line count | 198 |
| Word count | 2082 |
| Estimated token count (words / 0.75) | 2776 |
| Character count | 14192 |

---

## 3. Document Structure Depth

**All headings in order (with line numbers):**

| Line | Level | Heading |
|---|---|---|
| 7 | H1 | Brainstorm a Feature or Improvement |
| 19 | H2 | Core Principles |
| 28 | H2 | Interaction Rules |
| 35 | H2 | Output Guidance |
| 40 | H2 | Feature Description |
| 48 | H2 | Execution Flow |
| 50 | H3 | Phase 0: Resume, Assess, and Route |
| 52 | H4 | 0.1 Resume Existing Work When Appropriate |
| 59 | H4 | 0.1b Classify Task Domain |
| 73 | H4 | 0.2 Assess Whether Brainstorming Is Needed |
| 84 | H4 | 0.3 Assess Scope |
| 93 | H3 | Phase 1: Understand the Idea |
| 95 | H4 | 1.1 Existing Context Scan |
| 119 | H4 | 1.2 Product Pressure Test |
| 141 | H4 | 1.3 Collaborative Dialogue |
| 156 | H3 | Phase 2: Explore Approaches |
| 182 | H3 | Phase 3: Capture the Requirements |
| 188 | H3 | Phase 3.5: Document Review |
| 196 | H3 | Phase 4: Handoff |

**Total headings:** 19
**Maximum depth:** H4 (level 4)

**Count per level:**
| Level | Count |
|---|---|
| H1 | 1 |
| H2 | 6 |
| H3 | 6 |
| H4 | 6 |

---

## 4. Content Specificity Assessment

**Rating: 5 / 5**

The skill is highly specific and operational. Instructions are written as executable directives, not vague goals. Decision logic is branched and conditional. Scope classifications (Lightweight/Standard/Deep) have differentiated behavior per classification. The document functions as a deterministic workflow, not a set of principles.

**Excerpt justifications:**

1. Phase 0.1b provides explicit routing logic with boolean conditions and labeled outcomes:
   > "Non-software brainstorming (route to universal brainstorming) -- BOTH conditions must be true: None of the software signals above are present / The task describes something the user wants to explore, decide, or think through in a non-software domain"

2. Phase 1.2 differentiates question sets by scope tier:
   > "Lightweight: Is this solving the real user problem? / Are we duplicating something that already covers this? [...] Standard: Is this the right problem, or a proxy for a more important one? [...] Deep -- Standard questions plus: What durable capability should this create in 6-12 months?"

3. Phase 1.1 contains a verification constraint with explicit labeling requirement:
   > "Any claim that something is absent -- a missing table, an endpoint that doesn't exist, a dependency not in the Gemfile, a config option with no current support -- must be verified against the codebase first; if not verified, label it as an unverified assumption."

---

## 5. Internal File References

References found in SKILL.md:

| Reference | Location in SKILL.md |
|---|---|
| `references/universal-brainstorming.md` | Phase 0.1b (non-software routing) |
| `references/requirements-capture.md` | Phase 3 (capture requirements) |
| `references/handoff.md` | Phase 4 (handoff) |

No references to `references/visual-communication.md` in SKILL.md directly; it is referenced from within `references/requirements-capture.md` ("Read `references/visual-communication.md`").

---

## 6. Skill Cross-References

References to other skills found in SKILL.md:

| Reference | Context |
|---|---|
| `document-review` | Phase 3.5: "run the `document-review` skill on it before presenting handoff options" |

Implicit skill reference via slash command (not a skill load):
| Reference | Context |
|---|---|
| `/ce:plan` | Multiple locations -- recommended next step after brainstorm |
| `/ce:brainstorm` | Self-reference -- resume instruction |

---

## 7. Agent References

| Agent | Context |
|---|---|
| `compound-engineering:research:slack-researcher` | Phase 1.1 Slack context block -- dispatched when tools available and user requests Slack context |

The dispatch is conditional and opt-in. Three branches are specified: tools available + user asked (dispatch), tools available + user didn't ask (surface offer), no tools + user asked (surface error).

---

## 8. Other Markdown File Analysis

### references/handoff.md

| Metric | Value |
|---|---|
| Bytes | 4424 |
| Lines | 94 |
| Words | 646 |
| Estimated tokens | 861 |

**Headings:**
| Line | Level | Heading |
|---|---|---|
| 1 | H1 | Handoff |
| 7 | H4 | 4.1 Present Next-Step Options |
| 31 | H4 | 4.2 Handle the Selected Option |
| 64 | H4 | 4.3 Closing Summary |

Note: heading levels jump from H1 to H4 with no H2/H3 intermediaries. This appears intentional -- the file is loaded mid-workflow at Phase 4, continuing the parent document's heading hierarchy.

Contains 1 code block (bash curl command for "Share to Proof" option). Contains 2 inline code text blocks (closing summary templates).

Skill cross-references in this file: `document-review` (load for additional review pass), `/ce:plan` (dispatch), `/ce:work` (dispatch), `proof` skill (load for Share to Proof).

---

### references/requirements-capture.md

| Metric | Value |
|---|---|
| Bytes | 5666 |
| Lines | 104 |
| Words | 826 |
| Estimated tokens | 1101 |

**Headings:**
| Line | Level | Heading |
|---|---|---|
| 1 | H1 | Requirements Capture |
| 32 | H1 | \<Topic Title\> (template heading) |
| 34 | H2 | Problem Frame |
| 37 | H2 | Requirements |
| 46 | H2 | Success Criteria |
| 49 | H2 | Scope Boundaries |
| 52 | H2 | Key Decisions |
| 55 | H2 | Dependencies / Assumptions |
| 58 | H2 | Outstanding Questions |
| 60 | H3 | Resolve Before Planning |
| 63 | H3 | Deferred to Planning |
| 67 | H2 | Next Steps |

Note: line 32's H1 is inside a fenced code block (the document template), not a real document heading.

Contains 1 large fenced code block (full requirements document template with YAML frontmatter).

References `references/visual-communication.md` explicitly.

Contains a pre-finalization checklist (7 bullet verification questions).

---

### references/universal-brainstorming.md

| Metric | Value |
|---|---|
| Bytes | 4528 |
| Lines | 52 |
| Words | 696 |
| Estimated tokens | 928 |

**Headings:**
| Line | Level | Heading |
|---|---|---|
| 1 | H1 | Universal Brainstorming Facilitator |
| 7 | H2 | Your role |
| 13 | H2 | How to start |
| 26 | H2 | How to explore and generate |
| 40 | H2 | How to converge |
| 44 | H2 | When to wrap up |

Loaded only when Phase 0.1b routes to non-software brainstorming. Replaces the software workflow entirely. Contains no file references. References `/ce:plan`, `proof` skill, `AskUserQuestion`/`request_user_input`/`ask_user` platform question tools.

Scope tiers defined here (Quick/Standard/Full) differ in naming from SKILL.md tiers (Lightweight/Standard/Deep) -- consistent in concept, different labels.

---

### references/visual-communication.md

| Metric | Value |
|---|---|
| Bytes | 2881 |
| Lines | 29 |
| Words | 425 |
| Estimated tokens | 567 |

**Headings:**
| Line | Level | Heading |
|---|---|---|
| 1 | H1 | Visual Communication in Requirements Documents |

Single H1, no subheadings. Content is delivered entirely as a decision table and bulleted rules.

Contains 1 markdown table (4 rows, 3 columns: content pattern, visual aid type, placement rule). Contains no code blocks. Contains no cross-references to other skills or agents.

---

## 9. Structural Observations

### YAML Frontmatter (SKILL.md)

Present. Fields used:
- `name`: `ce:brainstorm`
- `description`: 560-character multi-trigger description covering explicit and implicit invocation signals
- `argument-hint`: `[feature idea or problem to explore]`

No `tools`, `color`, or `model` fields present.

### Code Blocks

SKILL.md: 0 fenced code blocks. All content is prose, bullets, and bold-labeled rules.

Reference files:
- `handoff.md`: 1 bash block (curl for Proof share), 2 template text blocks
- `requirements-capture.md`: 1 large fenced code block (full document template with YAML frontmatter, all section headers, placeholder content)
- `universal-brainstorming.md`: 0 code blocks
- `visual-communication.md`: 0 code blocks

### Lists vs. Prose

SKILL.md is mixed: section headers with numbered bullet lists for principles and rules (Core Principles, Interaction Rules, Output Guidance), then mostly prose paragraphs with embedded bullets for phase instructions. Phases use bold-labeled inline terms rather than sub-bullets. Heavy use of bold for term labels (`**Lightweight**`, `**Standard**`, `**Deep**`).

Reference files lean toward prose (`handoff.md`, `universal-brainstorming.md`) or mixed with a template block (`requirements-capture.md`). `visual-communication.md` is almost entirely structured (table + bullet rules).

### Conditional Logic

SKILL.md contains extensive branching:
- Phase 0.1b: 3-way domain classification (software / non-software / neither)
- Phase 0.2: 2-way branch (clear requirements vs. ambiguous)
- Phase 0.3: 3-way scope classification (Lightweight / Standard / Deep)
- Phase 1.1: 3-way Slack context branch (tools + asked / tools + not asked / no tools + asked)
- Phase 1.2: scope-differentiated question sets
- Phase 2: conditional approach menu vs. direct recommendation
- Phase 3: conditional document creation by scope

`handoff.md` adds: blocking-question gate for "Proceed to planning" and "Proceed directly to work"; 6-way option handling with mutual exclusion conditions.

### Templates

`requirements-capture.md` contains a complete document template as a fenced code block. The template includes YAML frontmatter, all section headers with placeholder content, requirement ID patterns (`R1`, `R2`), and tagging conventions (`[Affects R1]`, `[User decision]`, `[Technical]`, `[Needs research]`).

`handoff.md` contains two closing summary templates (success path and blocked/paused path) as fenced text blocks.

### Examples

SKILL.md provides inline examples for file path format (`src/models/user.rb`), scope classification triggers, and question examples per phase. No extended worked examples.

`requirements-capture.md` provides example requirement group headers (`"Packaging"`, `"Migration and Compatibility"`, `"Contributor Workflow"`).

### Constraints

Explicit hard constraints in SKILL.md:
1. All file references must use repo-relative paths, never absolute -- stated twice (Core Principles + Output Guidance)
2. Ask one question at a time -- stated in Interaction Rules and repeated in Phase 1.3
3. Claims about absent infrastructure must be verified or labeled as unverified assumptions
4. Do not include implementation details in requirements documents unless the brainstorm is itself architectural
5. Do not offer "Proceed directly to work" unless 4 gate conditions are all satisfied (scope lightweight + success criteria clear + scope boundaries clear + no meaningful technical/research questions remain)

Platform-specific tooling noted as conditional: `AskUserQuestion` (Claude Code), `request_user_input` (Codex), `ask_user` (Gemini) -- skill is designed for multi-platform deployment.

### Lazy Loading Pattern

Three of four reference files are loaded conditionally at runtime (not at skill load):
- `references/universal-brainstorming.md` -- loaded only on non-software route
- `references/requirements-capture.md` -- loaded at Phase 3 entry
- `references/handoff.md` -- loaded at Phase 4 entry

`references/visual-communication.md` is one step further removed -- it is referenced from within `requirements-capture.md`, not from SKILL.md directly. Effective load depth: SKILL.md -> requirements-capture.md -> visual-communication.md.
