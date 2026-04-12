# Skill Analysis: brand-guidelines

**Repository:** anthropics/skills  
**Branch:** main  
**Skill path:** skills/brand-guidelines  
**Analysis date:** 2026-04-11

---

## 1. Overview

**Skill name (directory):** `brand-guidelines`  
**Skill name (SKILL.md frontmatter `name:`):** `brand-guidelines`  
**Skill title text (`# Title` line):** `# Anthropic Brand Styling`  
**Title character length (including `# ` prefix):** 25  
**Title character length (text only, excluding `# `):** 23  

**Skill description (from YAML frontmatter `description:` field):**  
`Applies Anthropic's official brand colors and typography to any sort of artifact that may benefit from having Anthropic's look-and-feel. Use it when brand colors or style guidelines, visual formatting, or company design standards apply.`  
**Description character length (value only, excluding `description: ` key):** 241  

**Total number of files in skill directory (recursive):** 2  
**Total number of subdirectories:** 0  

**All files with relative paths:**

| Relative Path | Size (bytes) | Type |
|---|---|---|
| `SKILL.md` | 2235 | file |
| `LICENSE.txt` | 11357 | file |

---

## 2. SKILL.md Metrics

| Metric | Value |
|---|---|
| Line count | 73 |
| Word count | 281 |
| Estimated token count (word count / 0.75, rounded) | 375 |
| Character count (bytes) | 2235 |

**Method notes:**
- Line count: 73 lines (lines 1-73, no blank trailing line)
- Word count: 281 (counted from raw text including frontmatter)
- Character count: 2235 bytes per GitHub API `size` field
- Token estimate: 281 / 0.75 = 374.67, rounded to 375

---

## 3. Document Structure Depth

**All headings in document order (with line numbers):**

| Line | Level | Text |
|---|---|---|
| 7 | H1 | `Anthropic Brand Styling` |
| 9 | H2 | `Overview` |
| 15 | H2 | `Brand Guidelines` |
| 17 | H3 | `Colors` |
| 32 | H3 | `Typography` |
| 38 | H2 | `Features` |
| 40 | H3 | `Smart Font Application` |
| 47 | H3 | `Text Styling` |
| 54 | H3 | `Shape and Accent Colors` |
| 60 | H2 | `Technical Details` |
| 62 | H3 | `Font Management` |
| 69 | H3 | `Color Application` |

**Maximum heading depth reached:** H3 (level 3)

**Heading count per level:**

| Level | Count |
|---|---|
| H1 | 1 |
| H2 | 4 |
| H3 | 7 |
| H4 | 0 |
| H5 | 0 |
| H6 | 0 |

**Total headings:** 12

---

## 4. Content Specificity Assessment

**Score: 4 / 5**

**Justification:**  
The skill provides precise, actionable brand values with exact hex color codes (`#141413`, `#faf9f5`, `#b0aea5`, `#e8e6dc`, `#d97757`, `#6a9bcc`, `#788c5d`), specific named typefaces with fallbacks (Poppins/Arial, Lora/Georgia), and concrete application rules (24pt threshold for heading font application, accent color cycling order). The implementation note referencing `python-pptx's RGBColor class` names a specific technical dependency. Deductions from a perfect 5: the "Smart Font Application" and "Text Styling" sections partially duplicate the same information (both list Poppins for headings 24pt+, Lora for body), and no concrete code examples or invocation patterns are included. The license field references `LICENSE.txt` without quoting the license type inline.

---

## 5. Internal File References (files referenced within SKILL.md)

| Referenced File | Location in SKILL.md | Exists in Skill Directory |
|---|---|---|
| `LICENSE.txt` | Line 4, frontmatter: `license: Complete terms in LICENSE.txt` | Yes |

---

## 6. Skill Cross-References

None. SKILL.md contains no references to other skills by name or path.

---

## 7. Agent References

None. SKILL.md contains no references to agents.

---

## 8. Other Markdown File Analysis

No other markdown files exist in the skill directory. The only non-SKILL.md file is `LICENSE.txt` (Apache License 2.0, 11357 bytes), which is a plain text legal document, not a markdown file.

---

## 9. Structural Observations

**YAML frontmatter:**  
Present. Lines 1-5. Fields: `name`, `description`, `license`. No `version`, `author`, `tools`, or `trigger` fields. The `license` field uses an indirect reference (`Complete terms in LICENSE.txt`) rather than stating the license name directly (Apache 2.0).

**Code blocks:**  
None. Hex color values are wrapped in inline code ticks (e.g., `` `#141413` ``) but no fenced code blocks exist.

**Lists vs prose:**  
Heavily list-driven. Approximately 80% of the body content after the Overview paragraph is bullet lists. The Overview section (line 11) is the only complete prose sentence in the body. The Keywords line (line 13) is a bold-labeled inline list of terms.

**Conditional logic:**  
None explicit. The fallback font behavior ("falls back to Arial/Georgia if custom fonts unavailable") describes conditional runtime behavior but is stated as a prose bullet, not structured logic.

**Templates:**  
None.

**Examples:**  
None. No example invocations, sample outputs, or before/after illustrations.

**Constraints sections:**  
None explicitly labeled. The `**Note**` bullet under Typography (line 36) functions as a soft constraint ("Fonts should be pre-installed in your environment for best results") but is not structured as a constraints block.

**Duplication:**  
"Smart Font Application" (H3, lines 40-45) and "Text Styling" (H3, lines 47-52) overlap significantly. Both enumerate Poppins for headings and Lora for body text. "Text Styling" adds "Smart color selection based on background" and "Preserves text hierarchy and formatting" as distinct points, but the font rules are repeated verbatim in effect.

**Keywords annotation:**  
Line 13 contains an explicit `**Keywords**` field with 10 comma-separated terms. This is an informal trigger hint to the model, not a structured frontmatter field.

**Technical specificity:**  
The `python-pptx` library reference (line 72) implies the primary target artifact type is PowerPoint (`.pptx`) files, though this is never stated explicitly in the skill description or overview.
