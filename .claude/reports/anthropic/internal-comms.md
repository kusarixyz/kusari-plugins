# Skill Analysis: internal-comms

**Repository:** anthropics/skills  
**Branch:** main  
**Path:** skills/internal-comms  
**Analysis date:** 2026-04-11

---

## 1. Overview

**Skill name:** internal-comms  
**Title text (from YAML `name` field):** `internal-comms` (14 characters)  
**Description (from YAML `description` field):**  
> A set of resources to help me write all kinds of internal communications, using the formats that my company likes to use. Claude should use this skill whenever asked to write some sort of internal communications (status reports, leadership updates, 3P updates, company newsletters, FAQs, incident reports, project updates, etc.).

Description character length: 325 characters

**Total files (recursive):** 6  
**Subdirectories:** 1 (`examples/`)

**File list:**
```
skills/internal-comms/
  SKILL.md
  LICENSE.txt
  examples/
    3p-updates.md
    company-newsletter.md
    faq-answers.md
    general-comms.md
```

---

## 2. SKILL.md Metrics

SKILL.md raw content (32 lines, reproduced from verbatim fetch):

```
---
name: internal-comms
description: A set of resources to help me write all kinds of internal communications, using the formats that my company likes to use. Claude should use this skill whenever asked to write some sort of internal communications (status reports, leadership updates, 3P updates, company newsletters, FAQs, incident reports, project updates, etc.).
license: Complete terms in LICENSE.txt
---

## When to use this skill
To write internal communications, use this skill for:
- 3P updates (Progress, Plans, Problems)
- Company newsletters
- FAQ responses
- Status reports
- Leadership updates
- Project updates
- Incident reports

## How to use this skill

To write any internal communication:

1. **Identify the communication type** from the request
2. **Load the appropriate guideline file** from the `examples/` directory:
    - `examples/3p-updates.md` - For Progress/Plans/Problems team updates
    - `examples/company-newsletter.md` - For company-wide newsletters
    - `examples/faq-answers.md` - For answering frequently asked questions
    - `examples/general-comms.md` - For anything else that doesn't explicitly match one of the above
3. **Follow the specific instructions** in that file for formatting, tone, and content gathering

If the communication type doesn't match any existing guideline, ask for clarification or more context about the desired format.

## Keywords
3P updates, company newsletter, company comms, weekly update, faqs, common questions, updates, internal comms
```

| Metric | Value |
|--------|-------|
| Line count | 32 |
| Word count | ~230 (body ~107 + YAML description ~56 = ~163 excluding frontmatter body; total including frontmatter ~230) |
| Estimated token count (words / 0.75) | ~307 |
| Character count | ~1,511 (matches stated file size) |

Notes on word count methodology: YAML frontmatter included. Description field alone contributes ~57 words. Body (lines 7-32) contributes ~106 words. Total: ~163 words in meaningful prose/lists. Including YAML keys and punctuation tokens: ~230 words total.

---

## 3. Document Structure Depth

**Headings in order (body only, excluding YAML frontmatter):**

| Line | Level | Heading Text |
|------|-------|--------------|
| 7 | H2 | `When to use this skill` |
| 17 | H2 | `How to use this skill` |
| 31 | H2 | `Keywords` |

**Max depth:** H2 (level 2)  
**Count per level:**
- H1: 0
- H2: 3
- H3+: 0

**Headline breakdown:**
- Line 7: `## When to use this skill` - enumerates 7 communication types as a bullet list
- Line 17: `## How to use this skill` - 3-step numbered workflow with inline file references
- Line 31: `## Keywords` - comma-separated keyword string for trigger matching

No H1 heading. The skill name is conveyed only through YAML frontmatter. All content is flat at H2 depth.

---

## 4. Content Specificity Assessment

**Rating: 2 / 5**

The SKILL.md itself is a dispatch layer, not a content layer. It contains no formatting rules, tone guidance, workflow steps, or examples. Specificity lives entirely in the four referenced example files.

**Justifications:**

1. Excerpt (lines 21-26): The numbered workflow step 2 lists four files with one-line descriptions (`For Progress/Plans/Problems team updates`, `For company-wide newsletters`, etc.). These are category labels, not instructions. Zero actionable specificity in SKILL.md itself.

2. Excerpt (line 29): "If the communication type doesn't match any existing guideline, ask for clarification or more context about the desired format." This is a single fallback rule. It is precise but minimal -- one sentence covering all unclassified cases.

3. Excerpt (line 32): The keywords line (`3P updates, company newsletter, company comms, weekly update, faqs, common questions, updates, internal comms`) is a trigger-matching mechanism, not instructional content. It adds no behavioral specificity.

The skill's design is intentionally thin at the SKILL.md level and defers all specificity to `examples/`. This is architecturally valid but results in low standalone specificity for the root file.

---

## 5. Internal File References

All file references found in SKILL.md:

| Reference | Location | Context |
|-----------|----------|---------|
| `examples/3p-updates.md` | Line 23 | Maps to "Progress/Plans/Problems team updates" |
| `examples/company-newsletter.md` | Line 24 | Maps to "company-wide newsletters" |
| `examples/faq-answers.md` | Line 25 | Maps to "answering frequently asked questions" |
| `examples/general-comms.md` | Line 26 | Maps to "anything else that doesn't explicitly match one of the above" |
| `LICENSE.txt` | YAML line 4 (`license: Complete terms in LICENSE.txt`) | License reference in frontmatter |

Total internal file references: 5 (4 instructional, 1 license).

---

## 6. Skill Cross-References

None. SKILL.md contains no references to other skills, no `skills/` path references, and no cross-skill dependency declarations.

---

## 7. Agent References

None. SKILL.md contains no references to agents, subagents, or agent files.

---

## 8. Other Markdown File Analysis

### examples/3p-updates.md

**Sections (H2 headings):** Instructions, Tools Available, Workflow, Formatting  
**Line count:** ~47  
**Key content:**
- Defines 3P (Progress, Plans, Problems) format for executive audiences
- Specifies reading time target: 30-60 seconds
- Scales granularity by team size (small team vs. company-wide)
- Tools listed: Slack, Google Drive, Email, Calendar
- Workflow: 4 steps (Clarify scope, Gather information, Draft, Review)
- Strict output template:
  ```
  [emoji] [Team Name] (Dates Covered)
  Progress: [1-3 sentences]
  Plans: [1-3 sentences]
  Problems: [1-3 sentences]
  ```
- Requires emoji; requires metrics/data-driven tone; prohibits any other formatting

**Specificity:** High. Contains concrete format, length constraints, tone rules, temporal scoping for each section (past week / next week).

---

### examples/company-newsletter.md

**Sections (H2 headings):** Instructions, Tools to use, Sections, Prioritization, Example Formats  
**Line count:** ~67  
**Key content:**
- Target length: ~20-25 bullet points
- Distribution channel: Slack and email
- First-person plural voice ("we did this")
- Tools: Slack (high-reaction messages), Email (executive announcements), Calendar (large-attendee meetings), Documents (high-view docs), External press
- Breaks content into thematic sections for 1000+ person company
- Prioritization rules: company-wide impact, leadership announcements, major milestones; avoid granular team updates
- Example format template with 4 sections using emoji headers: Company Announcements, Progress on Priorities (with sub-bullets), Leadership Updates, Social Updates

**Specificity:** High. Contains length target, voice requirement, tool-specific search criteria, section structure, prioritization criteria, and a concrete output template.

---

### examples/faq-answers.md

**Sections (H2 headings):** Instructions, Tools Available, Formatting, Guidance, Answer Guidelines  
**Line count:** ~30  
**Key content:**
- Purpose: surface company-wide confusion points, not team-specific questions
- Tools: Slack (high-reaction questions), Email (existing FAQ emails), Documents (Google Drive, calendar-linked docs)
- Output format: italic-keyed Q&A pairs
  ```
  - *Question*: [1 sentence]
  - *Answer*: [1-2 sentences]
  ```
- Guidance: holistic company coverage, not user/team-centric
- Answer guidelines: base on official comms, flag uncertainty, link to sources, flag items needing executive input

**Specificity:** Medium-high. Format is explicit. Guidance is behavioral but not rigid.

---

### examples/general-comms.md

**Sections (H2 headings):** Instructions  
**Line count:** ~15 (estimated; content is sparse)  
**Key content:**
- Catch-all for communications not matching the other three templates
- Pre-flight checklist before proceeding: ask about target audience, purpose, tone (formal/casual/urgent/informational), formatting requirements
- General principles: clear and concise, active voice, most important information first, include links, match company style

**Specificity:** Low. Intentionally generic. No output template. No length constraints. Functions as a guardrail against proceeding without sufficient context, not as a formatting guide.

---

## 9. Structural Observations

### YAML Frontmatter
SKILL.md contains a valid YAML frontmatter block (lines 1-5):
```yaml
---
name: internal-comms
description: [325-character description with trigger guidance]
license: Complete terms in LICENSE.txt
---
```
Fields present: `name`, `description`, `license`. No `version`, `author`, or `tools` fields. The `description` field doubles as a trigger specification, explicitly naming the Claude invocation condition ("Claude should use this skill whenever asked to write some sort of internal communications").

### Code Blocks
SKILL.md: zero fenced code blocks. File references use inline backtick code spans only (e.g., `` `examples/3p-updates.md` ``).

Example files: `3p-updates.md` contains an implicit plaintext format template (not fenced). `company-newsletter.md` contains a multi-section template with emoji headers. Neither uses triple-backtick fencing.

### Lists vs. Prose
SKILL.md is predominantly list-driven:
- 7-item unordered list (communication types)
- 3-item numbered list (workflow steps) with 4-item nested unordered list (file mappings)
- 1 fallback sentence (prose)
- 1 keyword comma list

Prose content in SKILL.md is minimal -- approximately 2 full sentences outside of list items.

Example files are mixed: instructions sections use prose paragraphs; tools/formatting/workflow sections use bullet lists; formatting sections use pseudo-templates (plaintext or emoji-prefixed).

### Conditional Logic
One explicit conditional in SKILL.md (line 29): fall back to asking for clarification if communication type doesn't match any guideline.

`general-comms.md` encodes a pre-condition: ask 4 clarifying questions before proceeding. This is the most conditional behavior in the skill.

`3p-updates.md` includes a conditional: if tools not available, ask user directly.
`company-newsletter.md` mirrors this pattern identically.
`faq-answers.md` mirrors it as well.

All three tool-dependent files share the same fallback pattern: try tools, if unavailable ask user.

### Templates
Explicit output templates present in:
- `3p-updates.md`: strict 4-line format with emoji, team name, date, three sections
- `company-newsletter.md`: 4-section emoji-headered bullet structure
- `faq-answers.md`: italic-keyed Q&A pair format

`general-comms.md`: no template (by design, as it's a catch-all).

### Examples
No worked examples (filled-in sample outputs) in any file. Templates show structure placeholders only (e.g., `[1-3 sentences of content]`, `Announcement 1`). No concrete example with real content.

### Constraints
Explicit constraints found across example files:
- `3p-updates.md`: "Never use any formatting other than this"; 1-3 sentences per section; 30-60 second read time; data-driven/metrics required
- `company-newsletter.md`: ~20-25 bullet points; 1-2 sentences per bullet; "we" voice; avoid granular team updates
- `faq-answers.md`: 1 sentence question; 1-2 sentence answer; holistic company scope; flag uncertain information
- `general-comms.md`: must ask 4 questions before proceeding (implicit constraint on skipping ahead)

### Design Pattern
The skill follows a dispatch pattern: SKILL.md acts as a router that identifies the communication type and loads the appropriate sub-instruction file. This keeps the root file minimal and allows independent extension of each communication type without modifying SKILL.md. The `general-comms.md` catch-all prevents undefined behavior for unrecognized types.
