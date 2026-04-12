# Skill Analysis: frontend-design

**Repository:** anthropics/skills  
**Branch:** main  
**Path:** skills/frontend-design  
**Analysis date:** 2026-04-11

---

## 1. Overview

**Skill name:** frontend-design  
**Title text (from `name` frontmatter field):** `frontend-design`  
**Title char length:** 16

**Description (from `description` frontmatter field):**  
> Create distinctive, production-grade frontend interfaces with high design quality. Use this skill when the user asks to build web components, pages, artifacts, posters, or applications (examples include websites, landing pages, dashboards, React components, HTML/CSS layouts, or when styling/beautifying any web UI). Generates creative, polished code and UI design that avoids generic AI aesthetics.

**Description char length:** 393

**Total files (recursive):** 2  
**Subdirectories:** 0

**File list:**

| File | Size (bytes) | Type |
|------|-------------|------|
| LICENSE.txt | 10174 | file |
| SKILL.md | 4440 | file |

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Line count | 42 |
| Word count | ~510 |
| Estimated token count (words / 0.75) | ~680 |
| Character count | ~4440 (per GitHub API size field) |

**Methodology notes:**
- Line count is based on the raw fetched content including frontmatter and all blank lines.
- Word count is a manual count of all tokens separated by whitespace across the full document body and frontmatter values.
- Token estimate uses the formula: word_count / 0.75.
- Character count uses the file size in bytes reported by the GitHub Contents API (4440), which is reliable for this predominantly ASCII document.

---

## 3. Document Structure Depth

**Headings in order (with line numbers):**

| Line | Level | Heading text |
|------|-------|-------------|
| 11 | H2 | Design Thinking |
| 27 | H2 | Frontend Aesthetics Guidelines |

**Max depth:** 2 (H2 only)

**Count per level:**

| Level | Count |
|-------|-------|
| H1 | 0 |
| H2 | 2 |
| H3 | 0 |
| H4+ | 0 |

**Headline breakdown:**

- **Line 11 — `## Design Thinking`**: Covers pre-coding context gathering, aesthetic direction selection, and implementation intent. Contains 4 bullet points plus one bold CRITICAL note and a 4-item implementation checklist.
- **Line 27 — `## Frontend Aesthetics Guidelines`**: Covers typography, color, motion, spatial composition, and background/visual details. Contains 5 bullet points followed by 3 standalone directive paragraphs (NEVER, Interpret, IMPORTANT, Remember).

---

## 4. Content Specificity Assessment

**Rating: 4 / 5**

The skill is operationally specific in its directives. It names concrete technologies, font families to avoid, specific CSS properties, and library names. It provides a typology of aesthetic directions and explicit anti-patterns. It stops short of a 5 because it contains no code examples, no worked examples of "before/after" aesthetic transformation, and no decision trees or structured templates for triggering behavior. The guidance is directive prose rather than structured execution scaffolding.

**Excerpt justifications:**

1. **Specific (technology + library names):**  
   > "Use Motion library for React when available. Focus on high-impact moments: one well-orchestrated page load with staggered reveals (animation-delay)..."  
   Names a specific library, a specific CSS property, and a specific interaction pattern rather than vague "add animations."

2. **Specific (named anti-patterns with examples):**  
   > "NEVER use generic AI-generated aesthetics like overused font families (Inter, Roboto, Arial, system fonts), cliched color schemes (particularly purple gradients on white backgrounds)..."  
   Calls out exact font names and an exact visual pattern to avoid.

3. **Less specific (aspirational prose without structure):**  
   > "Remember: Claude is capable of extraordinary creative work. Don't hold back, show what can truly be created when thinking outside the box and committing fully to a distinctive vision."  
   This closing sentence is motivational rather than operational and adds no executable instruction.

---

## 5. Internal File References

References to files within the skill directory found in SKILL.md:

| Reference | Location | Context |
|-----------|----------|---------|
| `LICENSE.txt` | Frontmatter, `license` field | `license: Complete terms in LICENSE.txt` |

No other internal file references appear in the body of SKILL.md.

---

## 6. Skill Cross-References

**None found.**

SKILL.md contains no references to other skills by name, path, or `skill:` syntax.

---

## 7. Agent References

**None found.**

SKILL.md contains no references to agents by name or path.

---

## 8. Other Markdown File Analysis

**No other markdown files exist in the skill directory.**

The only non-SKILL.md file is `LICENSE.txt` (10174 bytes), which is a plain text license file, not a markdown document. It is referenced once in the SKILL.md frontmatter via the `license` field but contains no skill-relevant content.

---

## 9. Structural Observations

**YAML frontmatter**  
Present. Fields:
- `name`: `frontend-design`
- `description`: 393-character trigger description covering web components, pages, artifacts, applications, dashboards, React, HTML/CSS.
- `license`: `Complete terms in LICENSE.txt` — points to the accompanying license file rather than embedding license text.

No `tools`, `model`, `args`, or other execution-control fields present.

**Code blocks**  
None. No fenced code blocks (` ``` `) appear anywhere in SKILL.md. Technology references (HTML/CSS/JS, React, Vue) are inline text only.

**Lists vs. prose balance**  
Mixed, weighted toward prose with embedded lists:
- 2 unordered bullet lists in "Design Thinking" (4 items + 4 items)
- 1 unordered bullet list in "Frontend Aesthetics Guidelines" (5 items, each containing substantial inline prose)
- 4 standalone directive paragraphs outside lists (CRITICAL, NEVER, Interpret, IMPORTANT, Remember)

**Bold emphasis usage**  
Heavy. Bold is used for:
- Bullet point labels (e.g., `**Purpose**`, `**Typography**`, `**Motion**`)
- Inline section-level directives (`**CRITICAL**`, `**IMPORTANT**`)

**Conditional logic**  
None structured. There is one conditional-flavored sentence:  
> "Maximalist designs need elaborate code... Minimalist or refined designs need restraint..."  
This is prose, not structured branching logic.

**Templates**  
None. No fill-in-the-blank structures, prompt templates, or output scaffolds are present.

**Examples**  
No worked examples. Aesthetic direction names (brutally minimal, retro-futuristic, art deco/geometric, etc.) function as a typology/menu rather than full examples. No before/after comparisons, no sample code, no sample output.

**Constraints**  
Explicit negative constraints (NEVER rules):
1. Do not use Inter, Roboto, Arial, or system fonts.
2. Do not use purple gradients on white backgrounds.
3. Do not use predictable layouts and cookie-cutter component patterns.
4. Do not converge on common choices like Space Grotesk across generations.

No performance constraints, no token budget constraints, no output format constraints.

**Trigger scope**  
The description field is broad: it fires on "web components, pages, artifacts, posters, or applications" and explicitly includes "when styling/beautifying any web UI." This is a wide trigger surface covering most frontend generation tasks.
