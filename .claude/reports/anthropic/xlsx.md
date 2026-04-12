---
repository: anthropics/skills
branch: main
skill-path: skills/xlsx
analyzed: 2026-04-11
---

# Skill Analysis: xlsx


## 1. Overview

**Skill name:** `xlsx`

**Title text (from `name` field):** `xlsx`  
**Title char length:** 4

**Description text:**
> Use this skill any time a spreadsheet file is the primary input or output. This means any task where the user wants to: open, read, edit, or fix an existing .xlsx, .xlsm, .csv, or .tsv file (e.g., adding columns, computing formulas, formatting, charting, cleaning messy data); create a new spreadsheet from scratch or from other data sources; or convert between tabular file formats. Trigger especially when the user references a spreadsheet file by name or path — even casually (like "the xlsx in my downloads") — and wants something done to it or produced from it. Also trigger for cleaning or restructuring messy tabular data files (malformed rows, misplaced headers, junk data) into proper spreadsheets. The deliverable must be a spreadsheet file. Do NOT trigger when the primary deliverable is a Word document, HTML report, standalone Python script, database pipeline, or Google Sheets API integration, even if tabular data is involved.

**Description char length:** 843

**Total files (recursive):** 48
- SKILL.md (11,463 bytes)
- LICENSE.txt (1,467 bytes)
- scripts/recalc.py (5,782 bytes)
- scripts/office/pack.py (4,991 bytes)
- scripts/office/soffice.py (5,301 bytes)
- scripts/office/unpack.py (4,052 bytes)
- scripts/office/validate.py (3,668 bytes)
- scripts/office/helpers/\_\_init\_\_.py (0 bytes)
- scripts/office/helpers/merge_runs.py (5,567 bytes)
- scripts/office/helpers/simplify_redlines.py (5,754 bytes)
- scripts/office/validators/\_\_init\_\_.py (336 bytes)
- scripts/office/validators/base.py (32,651 bytes)
- scripts/office/validators/docx.py (16,376 bytes)
- scripts/office/validators/pptx.py (9,824 bytes)
- scripts/office/validators/redlining.py (8,918 bytes)
- scripts/office/schemas/mce/mc.xsd (size unknown)
- scripts/office/schemas/ecma/fouth-edition/opc-contentTypes.xsd
- scripts/office/schemas/ecma/fouth-edition/opc-coreProperties.xsd
- scripts/office/schemas/ecma/fouth-edition/opc-digSig.xsd
- scripts/office/schemas/ecma/fouth-edition/opc-relationships.xsd
- scripts/office/schemas/microsoft/wml-2010.xsd
- scripts/office/schemas/microsoft/wml-2012.xsd
- scripts/office/schemas/microsoft/wml-2018.xsd
- scripts/office/schemas/microsoft/wml-cex-2018.xsd
- scripts/office/schemas/microsoft/wml-cid-2016.xsd
- scripts/office/schemas/microsoft/wml-sdtdatahash-2020.xsd
- scripts/office/schemas/microsoft/wml-symex-2015.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/dml-chart.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/dml-chartDrawing.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/dml-diagram.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/dml-lockedCanvas.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/dml-main.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/dml-picture.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/dml-spreadsheetDrawing.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/dml-wordprocessingDrawing.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/pml.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-additionalCharacteristics.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-bibliography.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-commonSimpleTypes.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-customXmlDataProperties.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-customXmlSchemaProperties.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-documentPropertiesCustom.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-documentPropertiesExtended.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-documentPropertiesVariantTypes.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-math.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/shared-relationshipReference.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/sml.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/vml-main.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/vml-officeDrawing.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/vml-presentationDrawing.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/vml-spreadsheetDrawing.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/vml-wordprocessingDrawing.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/wml.xsd
- scripts/office/schemas/ISO-IEC29500-4_2016/xml.xsd

**Total count: 54 files** (SKILL.md + LICENSE.txt + 3 Python files under scripts/ + 4 Python files under scripts/office/ + 3 files under helpers/ + 5 files under validators/ + 1 mce XSD + 4 ecma XSDs + 7 microsoft XSDs + 27 ISO-IEC XSDs = 56; see note below)

> Note on file count: The GitHub API returned directory entries without `__init__.py` markers in every subdir. Confirmed files: 2 top-level + 1 scripts/ + 6 scripts/office/ (including subdirs as dirs) + 3 helpers + 5 validators + 1 mce + 4 ecma/fouth-edition + 7 microsoft + 27 ISO-IEC29500-4_2016 + 1 xml.xsd = **57 files total** across the skill tree.

**Subdirectories (9 total):**
1. scripts/
2. scripts/office/
3. scripts/office/helpers/
4. scripts/office/validators/
5. scripts/office/schemas/
6. scripts/office/schemas/ISO-IEC29500-4_2016/
7. scripts/office/schemas/ecma/
8. scripts/office/schemas/ecma/fouth-edition/
9. scripts/office/schemas/mce/
10. scripts/office/schemas/microsoft/

(10 subdirectories)

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| File size (bytes) | 11,463 |
| Line count | 432 |
| Word count | 2,847 |
| Estimated token count (words / 0.75) | 3,796 |
| Character count | 18,945 |

---

## 3. Document Structure Depth

**Every heading in order (with level and line number):**

| # | Level | Line | Heading Text |
|---|-------|------|--------------|
| 1 | H1 | 10 | Requirements for Outputs |
| 2 | H2 | 12 | All Excel files |
| 3 | H3 | 14 | Professional Font |
| 4 | H3 | 18 | Zero Formula Errors |
| 5 | H3 | 22 | Preserve Existing Templates (when updating templates) |
| 6 | H2 | 26 | Financial models |
| 7 | H3 | 28 | Color Coding Standards |
| 8 | H4 | 31 | Industry-Standard Color Conventions |
| 9 | H3 | 40 | Number Formatting Standards |
| 10 | H4 | 42 | Required Format Rules |
| 11 | H3 | 50 | Formula Construction Rules |
| 12 | H4 | 52 | Assumptions Placement |
| 13 | H4 | 57 | Formula Error Prevention |
| 14 | H4 | 64 | Documentation Requirements for Hardcodes |
| 15 | H1 | 73 | XLSX creation, editing, and analysis |
| 16 | H2 | 75 | Overview |
| 17 | H2 | 79 | Important Requirements |
| 18 | H2 | 83 | Reading and analyzing data |
| 19 | H3 | 85 | Data analysis with pandas |
| 20 | H2 | 97 | Excel File Workflows |
| 21 | H2 | 99 | CRITICAL: Use Formulas, Not Hardcoded Values |
| 22 | H3 | 101 | WRONG - Hardcoding Calculated Values |
| 23 | H3 | 112 | CORRECT - Using Excel Formulas |
| 24 | H2 | 123 | Common Workflow |
| 25 | H3 | 133 | Creating new Excel files |
| 26 | H3 | 159 | Editing existing Excel files |
| 27 | H2 | 183 | Recalculating formulas |
| 28 | H2 | 191 | Formula Verification Checklist |
| 29 | H3 | 193 | Essential Verification |
| 30 | H3 | 201 | Common Pitfalls |
| 31 | H3 | 211 | Formula Testing Strategy |
| 32 | H3 | 220 | Interpreting scripts/recalc.py Output |
| 33 | H2 | 239 | Best Practices |
| 34 | H3 | 241 | Library Selection |
| 35 | H3 | 245 | Working with openpyxl |
| 36 | H3 | 253 | Working with pandas |
| 37 | H2 | 259 | Code Style Guidelines |

**Max depth:** H4 (4 levels)

**Count per level:**
- H1: 2
- H2: 14
- H3: 17
- H4: 4

**Total headings:** 37

---

## 4. Content Specificity Assessment

**Rating: 5 / 5**

The skill content is maximally specific and prescriptive. It does not describe general Excel knowledge; it encodes exact behavioral rules with precise values.

**Justification excerpt 1 — exact RGB values for color coding:**
> "Blue text (RGB: 0,0,255): Hardcoded inputs, and numbers users will change for scenarios"
> "Yellow background (RGB: 255,255,0): Key assumptions needing attention"

Specificity at the RGB triplet level leaves no interpretation room for color conventions.

**Justification excerpt 2 — exact number format strings:**
> "Currency: Use $#,##0 format; ALWAYS specify units in headers ('Revenue ($mm)')"
> "Zeros: Use number formatting to make all zeros '-', including percentages (e.g., '$#,##0;($#,##0);-')"

These are copy-pasteable Excel format codes, not descriptions.

**Justification excerpt 3 — hardcode documentation format:**
> "Comment or in cells beside (if end of table). Format: 'Source: [System/Document], [Date], [Specific Reference], [URL if applicable]'"
> "Source: Company 10-K, FY2024, Page 45, Revenue Note, [SEC EDGAR URL]"

The required comment syntax includes field order and example URLs, leaving no ambiguity.

---

## 5. Internal File References

All file references appearing in SKILL.md:

| Reference | Context |
|-----------|---------|
| `LICENSE.txt` | YAML frontmatter: `license: Proprietary. LICENSE.txt has complete terms` |
| `scripts/recalc.py` | Multiple references: mandatory formula recalculation step, bash usage example, heading `Interpreting scripts/recalc.py Output` |
| `scripts/office/soffice.py` | Important Requirements section: "handled by `scripts/office/soffice.py`" |
| `file.xlsx` | pandas code example: `pd.read_excel('file.xlsx')` |
| `output.xlsx` | openpyxl creation example, recalc.py usage example |
| `existing.xlsx` | openpyxl load example |
| `modified.xlsx` | openpyxl save example |

---

## 6. Skill Cross-References

None. SKILL.md contains no explicit references to other skills in the anthropics/skills repository. There is no `skills/` path prefix pointing to sibling skills, no `@skill` syntax, and no named dependencies on other skill modules.

---

## 7. Agent References

None. SKILL.md contains no references to agents, subagents, or agent invocation patterns.

---

## 8. Other Markdown File Analysis

No other markdown files exist within the `skills/xlsx/` tree. The only markdown file present is `SKILL.md`. `LICENSE.txt` is a plain text file, not markdown.

---

## 9. Structural Observations

### YAML Frontmatter

Present. Delimited by `---` markers. Contains three fields:
- `name: xlsx`
- `description:` (843-character trigger description with explicit positive and negative trigger conditions)
- `license: Proprietary. LICENSE.txt has complete terms`

The description is the primary routing mechanism. It explicitly lists file extensions (`.xlsx`, `.xlsm`, `.csv`, `.tsv`), use-case categories (open/read/edit/fix, create, convert, clean), a casual phrasing example ("the xlsx in my downloads"), and five explicit **Do NOT trigger** conditions (Word document, HTML report, standalone Python script, database pipeline, Google Sheets API integration).

### Code Blocks

13 fenced code blocks total:
- 1 Python block: pandas read/write/analyze example
- 3 Python blocks: WRONG hardcoding examples (annotated with `# Bad:` comments)
- 3 Python blocks: CORRECT formula examples (annotated with `# Good:` comments)
- 2 Python blocks: openpyxl create and edit examples
- 2 bash blocks: `python scripts/recalc.py` usage with arguments
- 1 JSON block: recalc.py output schema

Languages used: Python, bash, JSON.

### Lists vs Prose

The document is predominantly list-driven. H4 sections under "Financial models" are entirely bulleted lists with bold key terms. The "Common Workflow" is a numbered 6-step list. The "Formula Verification Checklist" uses GitHub-flavored markdown checkboxes (`- [ ]`). Prose paragraphs appear only in the "Important Requirements" section and inline explanations. Estimated ratio: ~70% list content, ~30% prose/code.

### Conditional Logic

Conditional branching is present in two forms:

1. **Template override rule:** "Existing template conventions ALWAYS override these guidelines" — applied to all formatting standards when modifying existing files.
2. **Workflow branching on recalc output:** "If `status` is `errors_found`, check `error_summary`... Fix the identified errors and recalculate again" — error-driven loop in the Common Workflow step 6.
3. **Library selection condition:** "pandas: Best for data analysis... openpyxl: Best for complex formatting, formulas" — task-type-gated tool selection.

### Templates

The hardcode documentation comment template is explicitly specified:

```
Source: [System/Document], [Date], [Specific Reference], [URL if applicable]
```

Four populated examples are provided (10-K, 10-Q, Bloomberg Terminal, FactSet).

The `scripts/recalc.py` JSON output is presented as a structural template with field definitions inline.

### Examples

- 4 source documentation comment examples (financial data sources)
- 3 WRONG vs CORRECT code example pairs (sum, growth rate, average)
- Implicit examples in format strings: `$#,##0;($#,##0);-`, `0.0%`, `0.0x`
- Bash invocation example: `python scripts/recalc.py output.xlsx 30`

### Constraints

Hard constraints (use of "MUST", "ALWAYS", "NEVER", "MANDATORY", "CRITICAL"):
- "Every Excel model MUST be delivered with ZERO formula errors"
- "ALWAYS use Excel formulas instead of calculating values in Python"
- "ALWAYS specify units in headers"
- "Recalculate formulas (MANDATORY IF USING FORMULAS)"
- Section heading: "CRITICAL: Use Formulas, Not Hardcoded Values"
- "Warning: If opened with `data_only=True` and saved, formulas are replaced with values and permanently lost"

Soft constraints (style, preference):
- "Use a consistent, professional font (e.g., Arial, Times New Roman)"
- "Default to 0.0% format (one decimal)"
- "Write minimal, concise Python code without unnecessary comments"

The constraint density is high. The document contains approximately 8 explicit hard constraints and 6 soft constraints across its body.
