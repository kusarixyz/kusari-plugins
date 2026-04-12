---
repository: anthropics/skills
branch: main
skill-path: skills/docx
analyzed: 2026-04-11
---

# Skill Analysis: docx


## 1. Overview

**Skill name:** `docx`

**Title text:** `DOCX creation, editing, and analysis`
**Title char length:** 38

**Description:**
> Use this skill whenever the user wants to create, read, edit, or manipulate Word documents (.docx files). Triggers include: any mention of 'Word doc', 'word document', '.docx', or requests to produce professional documents with formatting like tables of contents, headings, page numbers, or letterheads. Also use when extracting or reorganizing content from .docx files, inserting or replacing images in documents, performing find-and-replace in Word files, working with tracked changes or comments, or converting content into a polished Word document. If the user asks for a 'report', 'memo', 'letter', 'template', or similar deliverable as a Word or .docx file, use this skill. Do NOT use for PDFs, spreadsheets, Google Docs, or general coding tasks unrelated to document generation.

**Description char length:** 645

**Total files (recursive):** 61

**Subdirectories (11):**
```
scripts/
scripts/office/
scripts/office/helpers/
scripts/office/schemas/
scripts/office/schemas/ISO-IEC29500-4_2016/
scripts/office/schemas/ecma/
scripts/office/schemas/ecma/fouth-edition/
scripts/office/schemas/mce/
scripts/office/schemas/microsoft/
scripts/office/validators/
scripts/templates/
```

**Full file list:**

| Path | Size |
|------|------|
| `LICENSE.txt` | 1,467 bytes |
| `SKILL.md` | 20,084 bytes |
| `scripts/__init__.py` | 1 byte |
| `scripts/accept_changes.py` | 4,051 bytes |
| `scripts/comment.py` | 10,694 bytes |
| `scripts/office/pack.py` | 4,991 bytes |
| `scripts/office/soffice.py` | 5,301 bytes |
| `scripts/office/unpack.py` | 4,052 bytes |
| `scripts/office/validate.py` | 3,668 bytes |
| `scripts/office/helpers/__init__.py` | 0 bytes |
| `scripts/office/helpers/merge_runs.py` | 5,567 bytes |
| `scripts/office/helpers/simplify_redlines.py` | 5,754 bytes |
| `scripts/office/schemas/ISO-IEC29500-4_2016/dml-chart.xsd` | 74,984 bytes |
| `scripts/office/schemas/ISO-IEC29500-4_2016/dml-chartDrawing.xsd` | 6,956 bytes |
| `scripts/office/schemas/ISO-IEC29500-4_2016/dml-diagram.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/dml-lockedCanvas.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/dml-main.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/dml-picture.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/dml-spreadsheetDrawing.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/dml-wordprocessingDrawing.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/pml.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-additionalCharacteristics.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-bibliography.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-commonSimpleTypes.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-customXmlDataProperties.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-customXmlSchemaProperties.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-documentPropertiesCustom.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-documentPropertiesExtended.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-documentPropertiesVariantTypes.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-math.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/shared-relationshipReference.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/sml.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/vml-main.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/vml-officeDrawing.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/vml-presentationDrawing.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/vml-spreadsheetDrawing.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/vml-wordprocessingDrawing.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/wml.xsd` | (not retrieved) |
| `scripts/office/schemas/ISO-IEC29500-4_2016/xml.xsd` | (not retrieved) |
| `scripts/office/schemas/ecma/fouth-edition/opc-contentTypes.xsd` | (not retrieved) |
| `scripts/office/schemas/ecma/fouth-edition/opc-coreProperties.xsd` | (not retrieved) |
| `scripts/office/schemas/ecma/fouth-edition/opc-digSig.xsd` | (not retrieved) |
| `scripts/office/schemas/ecma/fouth-edition/opc-relationships.xsd` | (not retrieved) |
| `scripts/office/schemas/mce/mc.xsd` | (not retrieved) |
| `scripts/office/schemas/microsoft/wml-2010.xsd` | (not retrieved) |
| `scripts/office/schemas/microsoft/wml-2012.xsd` | (not retrieved) |
| `scripts/office/schemas/microsoft/wml-2018.xsd` | (not retrieved) |
| `scripts/office/schemas/microsoft/wml-cex-2018.xsd` | (not retrieved) |
| `scripts/office/schemas/microsoft/wml-cid-2016.xsd` | (not retrieved) |
| `scripts/office/schemas/microsoft/wml-sdtdatahash-2020.xsd` | (not retrieved) |
| `scripts/office/schemas/microsoft/wml-symex-2015.xsd` | (not retrieved) |
| `scripts/office/validators/__init__.py` | 336 bytes |
| `scripts/office/validators/base.py` | 32,651 bytes |
| `scripts/office/validators/docx.py` | 16,376 bytes |
| `scripts/office/validators/pptx.py` | 9,824 bytes |
| `scripts/office/validators/redlining.py` | 8,918 bytes |
| `scripts/templates/comments.xml` | 2,603 bytes |
| `scripts/templates/commentsExtended.xml` | 2,611 bytes |
| `scripts/templates/commentsExtensible.xml` | 2,707 bytes |
| `scripts/templates/commentsIds.xml` | 2,619 bytes |
| `scripts/templates/people.xml` | 115 bytes |

Note: sizes for `.xsd` files beyond the first two were not individually retrieved; individual size data was truncated in API response.

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Character count | 20,084 |
| Line count | 590 |
| Word count | 2,612 |
| Estimated token count (words / 0.75) | 3,483 |

Note: The file size (20,084 bytes) matches the character count directly, indicating no multi-byte characters of significant count.

---

## 3. Document Structure Depth

### All headings in order with line numbers

Lines 32 and 35 appear in `grep -n "^#"` output but are bash comment lines (`# Text extraction...`, `# Raw XML access`) inside a fenced code block. They are **not markdown headings**. All actual markdown headings:

| Line | Level | Text |
|------|-------|------|
| 7 | H1 | `DOCX creation, editing, and analysis` |
| 9 | H2 | `Overview` |
| 13 | H2 | `Quick Reference` |
| 21 | H3 | `Converting .doc to .docx` |
| 29 | H3 | `Reading Content` |
| 39 | H3 | `Converting to Images` |
| 46 | H3 | `Accepting Tracked Changes` |
| 56 | H2 | `Creating New Documents` |
| 60 | H3 | `Setup` |
| 74 | H3 | `Validation` |
| 80 | H3 | `Page Size` |
| 116 | H3 | `Styles (Override Built-in Headings)` |
| 142 | H3 | `Lists (NEVER use unicode bullets)` |
| 176 | H3 | `Tables` |
| 223 | H3 | `Images` |
| 237 | H3 | `Page Breaks` |
| 247 | H3 | `Hyperlinks` |
| 270 | H3 | `Footnotes` |
| 291 | H3 | `Tab Stops` |
| 319 | H3 | `Multi-Column Layouts` |
| 352 | H3 | `Table of Contents` |
| 359 | H3 | `Headers/Footers` |
| 378 | H3 | `Critical Rules for docx-js` |
| 398 | H2 | `Editing Existing Documents` |
| 402 | H3 | `Step 1: Unpack` |
| 408 | H3 | `Step 2: Edit XML` |
| 436 | H3 | `Step 3: Pack` |
| 449 | H3 | `Common Pitfalls` |
| 456 | H2 | `XML Reference` |
| 458 | H3 | `Schema Compliance` |
| 464 | H3 | `Tracked Changes` |
| 530 | H3 | `Comments` |
| 556 | H3 | `Images` (duplicate heading name, different from line 223) |
| 585 | H2 | `Dependencies` |

**Total markdown headings:** 34

**Max depth:** H3 (3 levels)

**Count per level:**
- H1: 1
- H2: 7
- H3: 26

**H2 sections:**
1. Overview (line 9)
2. Quick Reference (line 13)
3. Creating New Documents (line 56)
4. Editing Existing Documents (line 398)
5. XML Reference (line 456)
6. Dependencies (line 585)

Note: The YAML frontmatter opens at line 1 (`---`) and the H1 appears at line 7, meaning the frontmatter spans lines 1-6.

---

## 4. Content Specificity Assessment

**Score: 5 / 5**

The skill operates at maximum specificity throughout. Every section provides actionable, implementation-ready content rather than conceptual guidance.

**Justification 1 — Exact numeric constants with unit explanation:**
> `width: 12240, height: 15840` — followed by the explicit note that `1,440 DXA = 1 inch`, and a full table of paper sizes with all three DXA column values spelled out. No vagueness about "set appropriate dimensions."

**Justification 2 — Anti-patterns named and shown with code:**
> The Lists section pairs `// WRONG` and `// CORRECT` blocks showing the exact unicode literal (`\u2022`) that must not be used alongside the exact `numbering.config` structure that replaces it. The prohibition is grounded in the technical reason (not a style preference).

**Justification 3 — Edge case behavior documented at XML level:**
> The Tracked Changes section documents the specific nesting required to delete an entire paragraph mark (`<w:del/>` inside `<w:pPr><w:rPr>`), explaining that omitting this leaves an empty paragraph/list item after accept. The "Rejecting another author's insertion" and "Restoring another author's deletion" patterns are spelled out as sibling XML structures with distinct author attribution.

---

## 5. Internal File References

All file references extracted from SKILL.md:

| Reference in SKILL.md | Type | Exists in repo |
|-----------------------|------|----------------|
| `scripts/office/soffice.py` | Python script (bash invocation) | Yes — `scripts/office/soffice.py` (5,301 bytes) |
| `scripts/office/unpack.py` | Python script (bash invocation) | Yes — `scripts/office/unpack.py` (4,052 bytes) |
| `scripts/office/validate.py` | Python script (bash invocation) | Yes — `scripts/office/validate.py` (3,668 bytes) |
| `scripts/office/pack.py` | Python script (bash invocation) | Yes — `scripts/office/pack.py` (4,991 bytes) |
| `scripts/comment.py` | Python script (bash invocation) | Yes — `scripts/comment.py` (10,694 bytes) |
| `scripts/accept_changes.py` | Python script (bash invocation) | Yes — `scripts/accept_changes.py` (4,051 bytes) |

**All 6 file references resolve to existing files.** No broken references. All are invoked via bash command examples, not imported as modules. No references to files outside the skill's own directory tree.

**Implicit references not via path strings:**
- `word/media/` — directory path within an unpacked .docx structure, not a skill repo file
- `word/_rels/document.xml.rels` — same, unpacked docx internal
- `[Content_Types].xml` — same

These are references to the internal structure of a .docx ZIP archive and are correctly not present as files in the skill repo.

---

## 6. Skill Cross-References

**None.** The SKILL.md contains zero references to other skills by name or path. The word "skill" appears only once in the document, in the YAML frontmatter `description` field (line 3), referring to the skill itself: `"Use this skill whenever..."`.

---

## 7. Agent References

**None.** The SKILL.md contains no references to any agent by name, path, or invocation pattern. The word "agent" does not appear in the document.

---

## 8. Other Markdown File Analysis

**No non-SKILL.md markdown files exist in the skill directory.** The full recursive file tree of 61 files contains:
- 1 `.md` file: `SKILL.md`
- 1 `.txt` file: `LICENSE.txt`
- Python files (`.py`): 11
- XML schema files (`.xsd`): 44
- XML template files (`.xml`): 5

There are no README.md, CHANGELOG.md, or other markdown files. Documentation is entirely self-contained in SKILL.md.

---

## 9. Structural Observations

### YAML Frontmatter

Present and well-formed. Three fields:
- `name: docx` — short identifier
- `description` — 645-character trigger description; includes positive triggers (Word doc, .docx, report, memo, etc.) and explicit negative triggers (PDFs, spreadsheets, Google Docs, general coding)
- `license: Proprietary. LICENSE.txt has complete terms` — inline pointer to LICENSE.txt

The description field is unusually long for a YAML frontmatter value but serves as the model's routing signal. It is syntactically a double-quoted string.

### Code Blocks

The document is code-block-heavy. Estimated 34+ fenced code blocks (```` ``` ````), covering:
- Bash command invocations (6 scripts)
- JavaScript (docx-js library usage): Setup, Page Size, Styles, Lists, Tables, Images, Page Breaks, Hyperlinks, Footnotes, Tab Stops, Multi-Column, TOC, Headers/Footers
- XML fragments: Tracked Changes (8 patterns), Comments (3 patterns), Images (4-step)
- One inline XML entity table (non-code, pipe table)

Code blocks account for a substantial majority of the document's character count. Most bash blocks are 1-4 lines; JavaScript blocks range from 5 to ~30 lines; XML blocks from 5 to ~20 lines.

### Lists vs Prose

The document has minimal free prose. Content is organized as:
- Fenced code blocks (dominant)
- Markdown tables (Quick Reference, page sizes, DXA unit reference, XML entity reference)
- Bullet lists: primarily the "Critical Rules for docx-js" section (18 bullet rules) and "Width rules" (5 bullets)
- Bold inline labels used as quasi-headers within sections (e.g., `**CRITICAL:**`, `**Auto-repair will fix:**`)

Prose paragraphs are sparse — most are 1-2 sentence introductions before a code block.

### Conditional Logic

No branching or conditional constructs in the skill text itself. Conditional behavior is implied by the workflow: "If validation fails, unpack, fix the XML, and repack." The `--validate false` and `--merge-runs false` flags on scripts represent optional code paths, documented inline.

### Templates

The `scripts/templates/` directory contains 5 XML templates used by `comment.py` at runtime:
- `comments.xml`
- `commentsExtended.xml`
- `commentsExtensible.xml`
- `commentsIds.xml`
- `people.xml`

These are not referenced by path in SKILL.md — they are implementation details of `comment.py`. The SKILL.md instructs using `comment.py` as a black box.

### Examples

Examples are embedded throughout via code blocks. Notable pattern: destructive anti-examples are shown before correct examples in the Lists and Tables sections, each labeled `// WRONG` / `// CORRECT` or `// BAD` / inline. The XML Reference section contains the densest example content — 8 distinct tracked-change patterns, each with minimal surrounding explanation.

### Constraints

Constraints are explicit and repeated for emphasis. The word "CRITICAL" appears 9 times in the document, each flagging a non-obvious rule that causes silent or hard-to-debug failures:
1. docx-js defaults to A4 (not US Letter)
2. Landscape: pass portrait dimensions
3. Tables need dual widths
4. Never use `WidthType.PERCENTAGE` (Google Docs incompatibility)
5. Use `ShadingType.CLEAR` not SOLID
6. Never use tables as dividers/rules in headers/footers
7. TOC requires HeadingLevel only
8. `ImageRun` requires explicit `type` parameter
9. `commentRangeStart`/`End` are siblings of `<w:r>`, never inside it

The `--** Do not write Python scripts.**` instruction in Step 2 is a behavioral constraint on the agent itself, not just the output format.

### Progressive Disclosure

The skill is structured for reference lookup, not sequential reading. The Quick Reference table at the top routes to three workflows (read, create, edit). Each workflow is self-contained. The XML Reference section is a deep reference that assumes the reader has already executed Steps 1-3. The Dependencies section at the end is minimal (4 tools listed with install commands).

### Duplication

The heading `Images` appears twice — at line 223 (docx-js `ImageRun` API) and line 556 (XML-level image embedding for the unpack/edit/repack workflow). These are correctly distinct: one for creation, one for editing. No content duplication detected between the two sections.
