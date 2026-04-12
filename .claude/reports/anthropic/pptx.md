# Skill Analysis: pptx

**Source:** `anthropics/skills` @ `main` — `skills/pptx/`
**Analysis date:** 2026-04-11

---

## 1. Overview

**Skill name:** pptx
**Title text:** `PPTX Skill` (10 chars)
**Description (inferred from Quick Reference table intro):** No YAML frontmatter exists; the skill has no formal `description` field. The nearest description is the implicit scope: reading, editing, and creating PowerPoint presentations using markitdown, XML manipulation, and PptxGenJS.

### Total Files (recursive)

| Path | Type | Size (bytes) |
|------|------|-------------|
| `LICENSE.txt` | file | 1,467 |
| `SKILL.md` | file | 9,182 |
| `editing.md` | file | 6,885 |
| `pptxgenjs.md` | file | 12,819 |
| `scripts/__init__.py` | file | 0 |
| `scripts/add_slide.py` | file | 6,872 |
| `scripts/clean.py` | file | 9,583 |
| `scripts/thumbnail.py` | file | 8,785 |
| `scripts/office/pack.py` | file | 4,991 |
| `scripts/office/soffice.py` | file | 5,301 |
| `scripts/office/unpack.py` | file | 4,052 |
| `scripts/office/validate.py` | file | 3,668 |
| `scripts/office/helpers/__init__.py` | file | 0 |
| `scripts/office/helpers/merge_runs.py` | file | 5,567 |
| `scripts/office/helpers/simplify_redlines.py` | file | 5,754 |
| `scripts/office/validators/__init__.py` | file | 336 |
| `scripts/office/validators/base.py` | file | 32,651 |
| `scripts/office/validators/docx.py` | file | 16,376 |
| `scripts/office/validators/pptx.py` | file | 9,824 |
| `scripts/office/validators/redlining.py` | file | 8,918 |
| `scripts/office/schemas/ISO-IEC29500-4_2016/` | dir | — |
| `scripts/office/schemas/ecma/` | dir | — |
| `scripts/office/schemas/mce/` | dir | — |
| `scripts/office/schemas/microsoft/` | dir | — |

**Total counted files (excluding schema dir contents, which are not enumerated):** 20 files

**Subdirectories:**
- `scripts/`
- `scripts/office/`
- `scripts/office/helpers/`
- `scripts/office/schemas/` (contains 4 further subdirs: `ISO-IEC29500-4_2016/`, `ecma/`, `mce/`, `microsoft/`)
- `scripts/office/validators/`

Total subdirectories (known): 9

---

## 2. SKILL.md Metrics

Raw file size: 9,182 bytes

Computed from content:

| Metric | Value |
|--------|-------|
| Line count | ~162 lines |
| Word count | ~1,290 words |
| Estimated token count (words / 0.75) | ~1,720 tokens |
| Character count | ~9,182 chars |

Methodology: word count estimated by counting space-delimited tokens in the fetched text; line count from visible newline structure; character count from reported file size.

---

## 3. Document Structure Depth

### SKILL.md Headings (in order)

| Line (approx) | Level | Heading Text |
|---------------|-------|--------------|
| 1 | H1 | `PPTX Skill` |
| 3 | H2 | `Quick Reference` |
| 13 | H2 | `Reading Content` |
| 22 | H2 | `Editing Workflow` |
| 29 | H2 | `Creating from Scratch` |
| 34 | H2 | `Design Ideas` |
| 36 | H3 | `Before Starting` |
| 43 | H3 | `Color Palettes` |
| 57 | H3 | `For Each Slide` |
| 71 | H3 | `Typography` |
| 84 | H3 | `Spacing` |
| 89 | H3 | `Avoid (Common Mistakes)` |
| 100 | H2 | `QA (Required)` |
| 102 | H3 | `Content QA` |
| 112 | H3 | `Visual QA` |
| 132 | H3 | `Verification Loop` |
| 142 | H2 | `Converting to Images` |
| 153 | H2 | `Dependencies` |

**Max depth:** H3 (3 levels)

**Count per level:**
- H1: 1
- H2: 9
- H3: 7

**Total headings:** 17

---

## 4. Content Specificity Assessment

**Score: 5 / 5**

The skill is operationally dense with no vague guidance. Every section contains executable commands, exact property names, or precise rules with rationale.

**Justification excerpts:**

1. **Exact bash commands with file paths:**
   > `python scripts/thumbnail.py presentation.pptx`
   > `python scripts/office/unpack.py presentation.pptx unpacked/`
   
   Commands are copy-paste ready with named scripts and argument positions.

2. **Color palette table with hex codes:**
   > `| **Midnight Executive** | 1E2761 (navy) | CADCFC (ice blue) | FFFFFF (white) |`
   
   Ten complete palettes with hex values tied to named themes — not generic advice.

3. **QA subagent prompt template with explicit checklist:**
   > `Look for: Overlapping elements (text through shapes, lines through words, stacked elements) / Text overflow or cut off at edges/box boundaries / Decorative lines positioned for single-line text but title wrapped to two lines ...`
   
   Fourteen specific visual defect categories listed, not general "check quality."

---

## 5. Internal File References

All references found in SKILL.md:

| Reference | Context | Exists in repo | Inside/Outside skill |
|-----------|---------|---------------|---------------------|
| `editing.md` | "Read [editing.md](editing.md) for full details." (Editing Workflow section) | Yes | Inside |
| `editing.md` | "Edit or create from template | Read [editing.md](editing.md)" (Quick Reference table) | Yes | Inside |
| `pptxgenjs.md` | "Create from scratch | Read [pptxgenjs.md](pptxgenjs.md)" (Quick Reference table) | Yes | Inside |
| `pptxgenjs.md` | "Read [pptxgenjs.md](pptxgenjs.md) for full details." (Creating from Scratch section) | Yes | Inside |
| `scripts/thumbnail.py` | Used in bash examples throughout | Yes | Inside |
| `scripts/office/unpack.py` | Used in bash example (Reading Content) | Yes | Inside |
| `scripts/office/soffice.py` | Used in bash example (Converting to Images) | Yes | Inside |
| `#converting-to-images` | Anchor link in Visual QA section: "see [Converting to Images](#converting-to-images)" | Yes (same doc) | Inside |

**All internal references resolve. No external file references. No broken links.**

---

## 6. Skill Cross-References

SKILL.md contains **no references to other skills** in the `anthropics/skills` repository. There are no `[skill:...]` tags, no references to `skills/` peer directories, and no mentions of other skill names (e.g., docx, pdf, etc.).

---

## 7. Agent References

SKILL.md contains **no references to named agents**. The word "subagent" appears three times:

1. In Visual QA: "**USE SUBAGENTS** — even for 2-3 slides. You've been staring at the code and will see what you expect, not what's there. Subagents have fresh eyes."
2. In the Verification Loop section (implied by the QA process).

These are generic architectural recommendations, not references to specific named agents.

---

## 8. Other Markdown File Analysis

### editing.md

**File size:** 6,885 bytes

| Metric | Value |
|--------|-------|
| Line count | ~143 lines |
| Word count | ~890 words |
| Estimated token count (words / 0.75) | ~1,187 tokens |
| Character count | ~6,885 chars |

**Headings (in order):**

| Level | Heading Text |
|-------|--------------|
| H1 | `Editing Presentations` |
| H2 | `Template-Based Workflow` |
| H2 | `Scripts` |
| H3 | `unpack.py` |
| H3 | `add_slide.py` |
| H3 | `clean.py` |
| H3 | `pack.py` |
| H3 | `thumbnail.py` |
| H2 | `Slide Operations` |
| H2 | `Editing Content` |
| H3 | `Formatting Rules` |
| H2 | `Common Pitfalls` |
| H3 | `Template Adaptation` |
| H3 | `Multi-Item Content` |
| H3 | `Smart Quotes` |
| H3 | `Other` |

**Max depth:** H3
**Total headings:** 16 (1× H1, 5× H2, 10× H3)

**Content specificity:** 5/5. Includes: step-by-step numbered workflow with 7 steps, per-script CLI reference table, named XML elements (`<p:sldIdLst>`, `<a:rPr>`, `<a:buChar>`), side-by-side wrong/correct XML code blocks with `b="1"` formatting rules, and a Unicode entity reference table for smart quotes.

**Internal file references in editing.md:**

| Reference | Exists | Notes |
|-----------|--------|-------|
| `scripts/thumbnail.py` | Yes | bash example |
| `scripts/office/unpack.py` | Yes | bash example |
| `scripts/add_slide.py` | Yes | bash examples (duplicate and layout forms) |
| `scripts/clean.py` | Yes | bash example |
| `scripts/office/pack.py` | Yes | bash example |
| `SKILL.md` | Yes | "For visual QA, use soffice + pdftoppm — see SKILL.md" |

All resolve. No broken references.

---

### pptxgenjs.md

**File size:** 12,819 bytes

| Metric | Value |
|--------|-------|
| Line count | ~295 lines |
| Word count | ~1,490 words |
| Estimated token count (words / 0.75) | ~1,987 tokens |
| Character count | ~12,819 chars |

**Headings (in order):**

| Level | Heading Text |
|-------|--------------|
| H1 | `PptxGenJS Tutorial` |
| H2 | `Setup & Basic Structure` |
| H2 | `Layout Dimensions` |
| H2 | `Text & Formatting` |
| H2 | `Lists & Bullets` |
| H2 | `Shapes` |
| H2 | `Images` |
| H3 | `Image Sources` |
| H3 | `Image Options` |
| H3 | `Image Sizing Modes` |
| H3 | `Calculate Dimensions (preserve aspect ratio)` |
| H3 | `Supported Formats` |
| H2 | `Icons` |
| H3 | `Setup` |
| H3 | `Add Icon to Slide` |
| H3 | `Icon Libraries` |
| H2 | `Slide Backgrounds` |
| H2 | `Tables` |
| H2 | `Charts` |
| H3 | `Better-Looking Charts` |
| H2 | `Slide Masters` |
| H2 | `Common Pitfalls` |
| H2 | `Quick Reference` |

**Max depth:** H3
**Total headings:** 23 (1× H1, 14× H2, 8× H3)

**Content specificity:** 5/5. Every section contains working JavaScript code blocks with exact API calls, property names, and values. Includes: shadow property constraints table with ranges and types; icon rasterization pipeline (React + sharp); aspect-ratio calculation formula; chart styling options dict. The Common Pitfalls section has 8 numbered antipatterns, 7 of which include side-by-side wrong/correct code examples.

**Internal file references in pptxgenjs.md:** None. This file is self-contained with no cross-references to other files in the skill.

---

## 9. Structural Observations

### YAML Frontmatter

**None.** SKILL.md, editing.md, and pptxgenjs.md all lack YAML frontmatter. There is no `title:`, `description:`, `tools:`, or `triggers:` block. This skill has no formal metadata declaration.

### Code Blocks

SKILL.md contains:
- 7 fenced code blocks: 4× `bash`, 1× generic (QA prompt template), 2 implicitly formatted (pip/npm install list at bottom shown as code)
- Code block content is executable (copy-paste ready commands)

editing.md contains:
- 8 fenced code blocks: 5× `bash`, 1× `xml` (wrong/correct pair shown in a non-fenced format with inline code)
- XML wrong/correct examples use fenced `xml` blocks

pptxgenjs.md contains:
- ~22 fenced code blocks: predominantly `javascript`, 1× shadow options table
- Every major API feature has an accompanying code example

### Lists vs. Prose

- SKILL.md is ~70% lists/tables, ~30% prose. Heavy use of markdown tables (Quick Reference, Color Palettes, Typography, Shadow options). Bullet lists dominate the Design Ideas and Avoid sections.
- editing.md is ~60% lists/code, ~40% prose with procedural steps.
- pptxgenjs.md is ~80% code blocks and tables, ~20% prose notes.

### Conditional Logic

SKILL.md contains explicit branching guidance:
- "When using templates, check for leftover placeholder text" (conditional QA step)
- "Use when no template or reference presentation is available" (path selection for pptxgenjs vs. editing workflow)

editing.md contains:
- "When source content has fewer items than the template" / "When replacing text with different length content" — explicit conditional branches with distinct instructions per case

### Templates

SKILL.md includes one reusable text template: the Visual QA subagent prompt block with `[placeholder]` fields:
```
1. /path/to/slide-01.jpg (Expected: [brief description])
```

editing.md includes no fill-in templates but provides structural patterns (XML paragraph templates for multi-item content).

### Examples

- pptxgenjs.md: ~22 inline code examples, 7 wrong/correct antipattern pairs
- editing.md: 2 wrong/correct XML antipattern pairs, smart quotes entity reference table
- SKILL.md: 10-row color palette table as concrete design examples

### Constraints (explicit prohibitions)

SKILL.md:
- "NEVER use accent lines under titles"
- "Don't create text-only slides"
- "Don't default to blue"
- "Don't center body text"

editing.md:
- "Never manually copy slide files"
- "Never use unicode bullets (•)"
- "Use the Edit tool, not sed or Python scripts"
- "Use `defusedxml.minidom`, not `xml.etree.ElementTree`"

pptxgenjs.md (Common Pitfalls, all marked with warning):
- "NEVER use '#' with hex colors"
- "NEVER encode opacity in hex color strings"
- "NEVER reuse option objects across calls"
- "Don't use ROUNDED_RECTANGLE with accent borders"
- "Avoid `lineSpacing` with bullets"

Total explicit prohibitions across all three files: ~20 distinct constraints.

### Process Ordering Enforcement

editing.md explicitly states: "**Complete all structural changes before step 5**" — enforcing a hard sequencing constraint between structural XML manipulation and content editing.

SKILL.md Verification Loop section enforces a non-skippable cycle: "**Do not declare success until you've completed at least one fix-and-verify cycle.**"
