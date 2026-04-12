# Skill Analysis: pdf

**Repository:** anthropics/skills | **Branch:** main | **Path:** skills/pdf

---

## 1. Overview

- **Skill name:** pdf
- **Title text (from H1 in SKILL.md):** "PDF Processing Guide" — 20 characters
- **Description (from YAML frontmatter):** "Use this skill whenever the user wants to do anything with PDF files. This includes reading or extracting text/tables from PDFs, combining or merging multiple PDFs into one, splitting PDFs apart, rotating pages, adding watermarks, creating new PDFs, filling PDF forms, encrypting/decrypting PDFs, extracting images, and OCR on scanned PDFs to make them searchable. If the user mentions a .pdf file or asks to produce one, use this skill." — 444 characters
- **Total files (recursive):** 13
- **Subdirectories:** 1 (`scripts/`)

### File list

| File | Size (bytes) | Location |
|------|-------------|----------|
| LICENSE.txt | 1467 | skills/pdf/ |
| SKILL.md | 8072 | skills/pdf/ |
| forms.md | 11854 | skills/pdf/ |
| reference.md | 16692 | skills/pdf/ |
| scripts/check_bounding_boxes.py | 2774 | skills/pdf/scripts/ |
| scripts/check_fillable_fields.py | 268 | skills/pdf/scripts/ |
| scripts/convert_pdf_to_images.py | 1008 | skills/pdf/scripts/ |
| scripts/create_validation_image.py | 1258 | skills/pdf/scripts/ |
| scripts/extract_form_field_info.py | 4300 | skills/pdf/scripts/ |
| scripts/extract_form_structure.py | 3945 | skills/pdf/scripts/ |
| scripts/fill_fillable_fields.py | 3819 | skills/pdf/scripts/ |
| scripts/fill_pdf_form_with_annotations.py | 3235 | skills/pdf/scripts/ |

Total: 12 files across 2 directories (skills/pdf/ root + scripts/).

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Line count | 314 |
| Word count | 1007 |
| Estimated token count (words / 0.75) | 1343 |
| Character count | 8072 |

---

## 3. Document Structure Depth

### SKILL.md headings (markdown only, outside code blocks)

| Line | Heading | Level |
|------|---------|-------|
| 7 | # PDF Processing Guide | H1 |
| 9 | ## Overview | H2 |
| 13 | ## Quick Start | H2 |
| 28 | ## Python Libraries | H2 |
| 30 | ### pypdf - Basic Operations | H3 |
| 32 | #### Merge PDFs | H4 |
| 46 | #### Split PDF | H4 |
| 56 | #### Extract Metadata | H4 |
| 66 | #### Rotate Pages | H4 |
| 79 | ### pdfplumber - Text and Table Extraction | H3 |
| 81 | #### Extract Text with Layout | H4 |
| 91 | #### Extract Tables | H4 |
| 102 | #### Advanced Table Extraction | H4 |
| 121 | ### reportlab - Create PDFs | H3 |
| 123 | #### Basic PDF Creation | H4 |
| 142 | #### Create PDF with Multiple Pages | H4 |
| 169 | #### Subscripts and Superscripts | H4 |
| 189 | ## Command-Line Tools | H2 |
| 191 | ### pdftotext (poppler-utils) | H3 |
| 203 | ### qpdf | H3 |
| 219 | ### pdftk (if available) | H3 |
| 231 | ## Common Tasks | H2 |
| 233 | ### Extract Text from Scanned PDFs | H3 |
| 252 | ### Add Watermark | H3 |
| 271 | ### Extract Images | H3 |
| 279 | ### Password Protection | H3 |
| 296 | ## Quick Reference | H2 |
| 309 | ## Next Steps | H2 |

Note: `#`-prefixed lines inside code blocks (Python comments such as `# Read a PDF`, `# Extract text`, etc.) are excluded. These appear throughout but are not document headings.

**Max depth:** H4 (level 4)

**Count per level:**

| Level | Count |
|-------|-------|
| H1 | 1 |
| H2 | 8 |
| H3 | 10 |
| H4 | 9 |
| **Total** | **28** |

---

## 4. Content Specificity Assessment

**Score: 4 / 5**

The skill is highly operational. It provides runnable code with real library names, exact method signatures, and concrete CLI flags. It stops short of 5 because it does not specify dependency versions, does not enumerate failure modes in SKILL.md itself (those are deferred to REFERENCE.md), and the Quick Reference table lists only tool-level choices without thresholds for when to prefer one over another.

**Excerpt justifications:**

1. **Specific CLI flags with semantics explained inline** (line 193-200):
   ```bash
   pdftotext -layout input.pdf output.txt
   pdftotext -f 1 -l 5 input.pdf output.txt  # Pages 1-5
   ```
   Flags are named and their purpose given, not generic placeholders.

2. **Explicit warning with concrete wrong values listed** (lines 170-188):
   > "Never use Unicode subscript/superscript characters (₀₁₂₃₄₅₆₇₈₉, ⁰¹²³⁴⁵⁶⁷⁸⁹) in ReportLab PDFs. The built-in fonts do not include these glyphs, causing them to render as solid black boxes."
   Specifies the exact character ranges and the failure mode.

3. **Quick Reference table** (lines 296-308) maps 8 tasks to specific tools and exact method/command fragments, giving an agent direct lookup rather than prose inference.

---

## 5. Internal File References

All references found in SKILL.md:

| Reference | Context in SKILL.md | Type | Exists in skill |
|-----------|--------------------|----- |----------------|
| `REFERENCE.md` | Overview section: "For advanced features, JavaScript libraries, and detailed examples, see REFERENCE.md." | Sibling file | Yes |
| `FORMS.md` | Overview section: "If you need to fill out a PDF form, read FORMS.md and follow its instructions." | Sibling file | Yes (filename is `forms.md`; case-insensitive match) |
| `REFERENCE.md` | Next Steps section: "For advanced pypdfium2 usage, see REFERENCE.md" | Sibling file | Yes |
| `REFERENCE.md` | Next Steps section: "For JavaScript libraries (pdf-lib), see REFERENCE.md" | Sibling file | Yes |
| `FORMS.md` | Next Steps section: "If you need to fill out a PDF form, follow the instructions in FORMS.md" | Sibling file | Yes |
| `REFERENCE.md` | Next Steps section: "For troubleshooting guides, see REFERENCE.md" | Sibling file | Yes |
| `FORMS.md` | Quick Reference table row: "Fill PDF forms | pdf-lib or pypdf (see FORMS.md) | See FORMS.md" | Sibling file | Yes |

**Summary:** 7 reference instances across 3 unique targets (REFERENCE.md x5, FORMS.md x3, counting Quick Reference table entry). All referenced files exist. No references to files outside the skill directory. No references to scripts/ from SKILL.md directly (scripts are only referenced from forms.md).

---

## 6. Skill Cross-References

SKILL.md contains no references to other skills in the anthropics/skills repository. There are no `@skill/`, `skills/`, or named cross-skill references anywhere in SKILL.md.

---

## 7. Agent References

SKILL.md contains no references to agents, subagents, or agent configuration. No `@agent`, agent tool invocations, or agent orchestration patterns appear.

---

## 8. Other Markdown File Analysis

### forms.md

| Metric | Value |
|--------|-------|
| Line count | 294 |
| Word count | 1649 |
| Estimated token count (words / 0.75) | 2199 |
| Character count | 11854 |

**Description:** A procedural workflow document for filling PDF forms. It is written as imperative step-by-step instructions addressed directly to an AI agent. It branches immediately based on whether the PDF has fillable form fields. For fillable PDFs it drives a JSON-mediated field extraction and fill pipeline. For non-fillable PDFs it provides three sub-approaches (Structure-Based, Visual Estimation, Hybrid) each with explicit coordinate system definitions, script commands, JSON schema examples, and coordinate conversion formulas.

**How referenced from SKILL.md:** Referenced 3 times. Once in the Overview section as a forward directive ("If you need to fill out a PDF form, read FORMS.md and follow its instructions"), once in the Quick Reference table cell ("See FORMS.md"), and once in the Next Steps section.

**Heading structure (markdown headings outside code blocks):**

| Line | Heading | Level |
|------|---------|-------|
| 6 | # Fillable fields | H1 |
| 78 | # Non-fillable fields | H1 |
| 81 | ## Step 1: Try Structure Extraction First | H2 |
| 96 | ## Approach A: Structure-Based Coordinates (Preferred) | H2 |
| 100 | ### A.1: Analyze the Structure | H3 |
| 111 | ### A.2: Check for Missing Elements | H3 |
| 120 | ### A.3: Create fields.json with PDF Coordinates | H3 |
| 163 | ### A.4: Validate Bounding Boxes | H3 |
| 172 | ## Approach B: Visual Estimation (Fallback) | H2 |
| 176 | ### B.1: Convert PDF to Images | H3 |
| 180 | ### B.2: Initial Field Identification | H3 |
| 189 | ### B.3: Zoom Refinement (CRITICAL for accuracy) | H3 |
| 224 | ### B.4: Create fields.json with Refined Coordinates | H3 |
| 247 | ### B.5: Validate Bounding Boxes | H3 |
| 256 | ## Hybrid Approach: Structure + Visual | H2 |
| 270 | ## Step 2: Validate Before Filling | H2 |
| 281 | ## Step 3: Fill the Form | H2 |
| 286 | ## Step 4: Verify Output | H2 |

Max depth: H3. H1: 2, H2: 7, H3: 9. Total: 18 headings.

The file has no YAML frontmatter. It opens directly with a bold `**CRITICAL:**` instruction block before the first heading.

---

### reference.md

| Metric | Value |
|--------|-------|
| Line count | 611 |
| Word count | 1893 |
| Estimated token count (words / 0.75) | 2524 |
| Character count | 16692 |

**Description:** An advanced reference document covering libraries and tools not included in SKILL.md. Covers: pypdfium2 (Python binding for PDFium/Chromium), two JavaScript libraries (pdf-lib and pdfjs-dist), advanced CLI usage for poppler-utils and qpdf (including encryption, optimization, repair), advanced Python usage of pdfplumber and reportlab, complex multi-step workflows (figure extraction, batch processing with error handling, advanced cropping), performance optimization tips, troubleshooting for encrypted/corrupted PDFs and OCR fallback, and a license summary table for all covered libraries.

**How referenced from SKILL.md:** Referenced 5 times in SKILL.md. Overview section: "For advanced features, JavaScript libraries, and detailed examples, see REFERENCE.md." Next Steps section (4 references): pypdfium2 advanced usage, JavaScript libraries, troubleshooting guides, and a general forward pointer.

**Heading structure (markdown headings outside code blocks):**

| Line | Heading | Level |
|------|---------|-------|
| 1 | # PDF Processing Advanced Reference | H1 |
| 5 | ## pypdfium2 Library (Apache/BSD License) | H2 |
| 7 | ### Overview | H3 |
| 10 | ### Render PDF to Images | H3 |
| 36 | ### Extract Text with pypdfium2 | H3 |
| 46 | ## JavaScript Libraries | H2 |
| 48 | ### pdf-lib (MIT License) | H3 |
| 52 | #### Load and Manipulate Existing PDF | H4 |
| 80 | #### Create Complex PDFs from Scratch | H4 |
| 141 | #### Advanced Merge and Split Operations | H4 |
| 170 | ### pdfjs-dist (Apache License) | H3 |
| 174 | #### Basic PDF Loading and Rendering | H4 |
| 208 | #### Extract Text with Coordinates | H4 |
| 244 | #### Extract Annotations and Forms | H4 |
| 265 | ## Advanced Command-Line Operations | H2 |
| 267 | ### poppler-utils Advanced Features | H3 |
| 269 | #### Extract Text with Bounding Box Coordinates | H4 |
| 277 | #### Advanced Image Conversion | H4 |
| 289 | #### Extract Embedded Images | H4 |
| 301 | ### qpdf Advanced Features | H3 |
| 303 | #### Complex Page Manipulation | H4 |
| 315 | #### PDF Optimization and Repair | H4 |
| 331 | #### Advanced Encryption | H4 |
| 343 | ## Advanced Python Techniques | H2 |
| 345 | ### pdfplumber Advanced Features | H3 |
| 347 | #### Extract Text with Precise Coordinates | H4 |
| 363 | #### Advanced Table Extraction with Custom Settings | H4 |
| 385 | ### reportlab Advanced Features | H3 |
| 387 | #### Create Professional Reports with Tables | H4 |
| 426 | ## Complex Workflows | H2 |
| 428 | ### Extract Figures/Images from PDF | H3 |
| 430 | #### Method 1: Using pdfimages (fastest) | H4 |
| 436 | #### Method 2: Using pypdfium2 + Image Processing | H4 |
| 463 | ### Batch PDF Processing with Error Handling | H3 |
| 509 | ### Advanced PDF Cropping | H3 |
| 528 | ## Performance Optimization Tips | H2 |
| 530 | ### 1. For Large PDFs | H3 |
| 535 | ### 2. For Text Extraction | H3 |
| 540 | ### 3. For Image Extraction | H3 |
| 544 | ### 4. For Form Filling | H3 |
| 548 | ### 5. Memory Management | H3 |
| 567 | ## Troubleshooting Common Issues | H2 |
| 569 | ### Encrypted PDFs | H3 |
| 582 | ### Corrupted PDFs | H3 |
| 589 | ### Text Extraction Issues | H3 |
| 603 | ## License Information | H2 |

Max depth: H4. H1: 1, H2: 8, H3: 17, H4: 19. Total: 45 headings.

---

## 9. Structural Observations

### YAML frontmatter

SKILL.md has a YAML frontmatter block (lines 1-5):
```yaml
---
name: pdf
description: Use this skill whenever...
license: Proprietary. LICENSE.txt has complete terms
---
```

Three keys: `name`, `description`, `license`. No `version`, `author`, or `tools` keys. `license` references LICENSE.txt but this is a plain string, not a file path pointer that the SDK would process.

forms.md and reference.md have no YAML frontmatter.

### Code blocks

SKILL.md contains a high density of fenced code blocks. Rough count: ~22 distinct fenced blocks covering Python (pypdf, pdfplumber, reportlab, pytesseract/pdf2image), bash (pdftotext, qpdf, pdftk, pdfimages), and one markdown table. Code blocks occupy approximately 180 of 314 lines (~57% of the file by line count).

reference.md is even more code-heavy: approximately 380 of 611 lines are inside fenced code blocks (~62%), covering Python, JavaScript (ES module syntax), and bash.

forms.md has fewer code blocks by proportion; it is more procedurally prose-driven with JSON schema examples embedded as fenced blocks. Approximately 120 of 294 lines are inside fenced blocks (~41%).

### Lists vs prose

SKILL.md: minimal prose paragraphs. The Overview section and "Subscripts and Superscripts" section contain the only substantive prose. Everything else is code or headings.

forms.md: significant prose in approach description and instruction steps, with numbered and bulleted lists for decision criteria (e.g., "Check the results" paragraph, "Common cases" bullets). This is the most prose-dense file.

reference.md: "Performance Optimization Tips" section uses bulleted lists. Most other content is code blocks under short prose sentences.

### Conditional logic

forms.md contains explicit branching logic visible to the executing agent:
- Top-level branch: fillable fields vs. non-fillable fields (run `check_fillable_fields.py` to decide)
- Second-level branch within non-fillable: Approach A (structure-based) vs. Approach B (visual) vs. Hybrid, with stated decision criteria
- Verification loop: Step 4 instructs the agent to check output and lists specific debugging steps per approach if text is mispositioned

SKILL.md has no conditional logic; it is a flat reference. reference.md has no conditional logic.

### Templates

forms.md contains two inline JSON schema templates:

1. `field_info.json` output schema (from `extract_form_field_info.py`): shows text, checkbox, radio_group, and choice field variants with all their properties.
2. `field_values.json` input schema (passed to `fill_fillable_fields.py`): shows the structure for providing fill values with field_id, description, page, and value.
3. `fields.json` schema for non-fillable approach (two variants): one for PDF coordinates using `pdf_width`/`pdf_height`, one for image coordinates using `image_width`/`image_height`.

SKILL.md contains one table template (Quick Reference, lines 296-308). reference.md contains no templates.

### Examples

SKILL.md: all code blocks are self-contained, runnable examples with inline comments. The Quick Reference table provides lookup examples.

forms.md: JSON examples are populated with realistic data ("Simpson", "Checkbox12", coordinate values like `[43, 63, 87, 73]`). ImageMagick crop command example includes concrete pixel values. Coordinate conversion formulas are written as equations with variable names.

reference.md: code blocks include realistic data (invoice line items, quarterly sales figures, filenames). The `extract_figures` function includes a comment acknowledging it is simplified.

### Constraints

Explicit constraints stated in the files:

1. **SKILL.md, lines 170-188:** "Never use Unicode subscript/superscript characters... in ReportLab PDFs." Hard prohibition with stated failure mode (renders as solid black boxes).
2. **forms.md, opening line:** "**CRITICAL: You MUST complete these steps in order. Do not skip ahead to writing code.**" Execution order constraint.
3. **forms.md, A.3:** "Important: Use `pdf_width`/`pdf_height` and coordinates directly from form_structure.json." Coordinate system constraint.
4. **forms.md, B.4:** "Important: Use `image_width`/`image_height` and the refined pixel coordinates from the zoom analysis." Coordinate system constraint.
5. **forms.md, Hybrid:** "Use a single coordinate system in fields.json" — requires all coordinates be converted to PDF space before writing the file.
6. **forms.md, Step 2 / A.4 / B.5:** Validation via `check_bounding_boxes.py` is mandated before filling — "Always validate bounding boxes before filling."
7. **reference.md, Performance Optimization Tips:** "Avoid `pypdf.extract_text()` for very large documents" — soft constraint with implicit threshold (no size number given).
