# Skill Analysis: theme-factory

**Repository:** anthropics/skills
**Branch:** main
**Skill path:** skills/theme-factory
**Analysis date:** 2026-04-11

---

## 1. Overview

**Skill name:** `theme-factory`

**Title text (from H1 in SKILL.md):** `Theme Factory Skill`
**Title char length:** 18

**Description (from frontmatter):**
`Toolkit for styling artifacts with a theme. These artifacts can be slides, docs, reportings, HTML landing pages, etc. There are 10 pre-set themes with colors/fonts that you can apply to any artifact that has been creating, or can generate a new theme on-the-fly.`
**Description char length:** 263

**Total files (recursive):** 13
- `LICENSE.txt` (11,357 bytes)
- `SKILL.md` (3,124 bytes)
- `theme-showcase.pdf` (124,310 bytes)
- `themes/arctic-frost.md` (544 bytes)
- `themes/botanical-garden.md` (519 bytes)
- `themes/desert-rose.md` (496 bytes)
- `themes/forest-canopy.md` (506 bytes)
- `themes/golden-hour.md` (528 bytes)
- `themes/midnight-galaxy.md` (513 bytes)
- `themes/modern-minimalist.md` (549 bytes)
- `themes/ocean-depths.md` (555 bytes)
- `themes/sunset-boulevard.md` (558 bytes)
- `themes/tech-innovation.md` (547 bytes)

**Subdirectories:** 1 (`themes/`)

---

## 2. SKILL.md Metrics

| Metric | Value |
|---|---|
| Line count | 59 |
| Word count | 486 |
| Estimated token count | 648 |
| Character count | 3,124 |

Token count formula: round(486 / 0.75) = 648.

---

## 3. Document Structure Depth

**Max depth:** H2 (2 levels used: H1 + H2)

**Heading count by level:**
- H1: 1
- H2: 6

**Total headings:** 7

**Headings in document order:**

| Line | Level | Text |
|---|---|---|
| 8 | H1 | Theme Factory Skill |
| 12 | H2 | Purpose |
| 19 | H2 | Usage Instructions |
| 28 | H2 | Themes Available |
| 43 | H2 | Theme Details |
| 50 | H2 | Application Process |
| 58 | H2 | Create your Own Theme |

---

## 4. Content Specificity Assessment

**Score: 4 — Mostly Specific**

The skill is action-oriented with concrete step sequences, explicit file references, and named resources. It stops short of 5 because it contains no CSS/HTML code samples and no color-token-level implementation detail within SKILL.md itself (those live in the theme files).

**Supporting excerpts:**

Line 21-25 (Usage Instructions — numbered steps with explicit file name):
> 1. **Show the theme showcase**: Display the `theme-showcase.pdf` file to allow users to see all available themes visually. Do not make any modifications to it; simply show the file for viewing.
> 2. **Ask for their choice**: Ask which theme to apply to the deck
> 3. **Wait for selection**: Get explicit confirmation about the chosen theme
> 4. **Apply the theme**: Once a theme has been chosen, apply the selected theme's colors and fonts to the deck/artifact

Line 51-55 (Application Process — concrete implementation steps):
> 1. Read the corresponding theme file from the `themes/` directory
> 2. Apply the specified colors and fonts consistently throughout the deck
> 3. Ensure proper contrast and readability
> 4. Maintain the theme's visual identity across all slides

Line 58 (Create your Own Theme — behavioral constraint):
> After generating the theme, show it for review and verification. Following that, apply the theme as described above.

---

## 5. Internal File References

| Reference | Type | Location in SKILL.md | Exists in skill dir |
|---|---|---|---|
| `theme-showcase.pdf` | Binary asset | Line 21, Line 30 | Yes — 124,310 bytes |
| `themes/` directory | Directory | Line 44, Line 51 | Yes |

Both references are inside the skill directory. No references point outside the skill boundary.

---

## 6. Skill Cross-References

None.

---

## 7. Agent References

None.

---

## 8. Other Markdown File Analysis

Ten theme definition files exist in `themes/`. All share an identical structure. Ocean Depths is representative; all others are structurally identical.

**Shared structure per theme file:**

| Element | Detail |
|---|---|
| H1 | Theme name |
| H2 | Color Palette |
| H2 | Typography |
| H2 | Best Used For |
| Lines | ~19 per file |
| Words | ~75-85 per file |
| Estimated tokens | ~100-113 per file |

**Per-file sizes (bytes) from tree API:**

| File | Bytes |
|---|---|
| ocean-depths.md | 555 |
| sunset-boulevard.md | 558 |
| modern-minimalist.md | 549 |
| tech-innovation.md | 547 |
| arctic-frost.md | 544 |
| golden-hour.md | 528 |
| midnight-galaxy.md | 513 |
| botanical-garden.md | 519 |
| forest-canopy.md | 506 |
| desert-rose.md | 496 |

**Theme file content pattern (same across all 10):**

Each theme file specifies:
- 4 named colors with hex codes (e.g., `#1a2332`)
- 2 font assignments: Headers font, Body Text font
- A "Best Used For" line listing 4-5 industry/context examples

**Font families used across themes:**

| Font | Themes using it |
|---|---|
| DejaVu Sans Bold (headers) | Ocean Depths, Arctic Frost, Modern Minimalist, Tech Innovation |
| DejaVu Sans (body) | Ocean Depths, Arctic Frost, Modern Minimalist, Tech Innovation, Forest Canopy, Botanical Garden |
| DejaVu Serif Bold (headers) | Sunset Boulevard, Botanical Garden |
| FreeSans Bold (headers) | Desert Rose, Golden Hour, Midnight Galaxy |
| FreeSans (body) | Desert Rose, Golden Hour, Midnight Galaxy, Forest Canopy |
| FreeSerif Bold (headers) | Forest Canopy |

---

## 9. Structural Observations

**YAML frontmatter:** Present. Fields: `name`, `description`, `license`. The `license` field points to `LICENSE.txt` with the note "Complete terms in LICENSE.txt" rather than embedding the license text.

**Code blocks:** None in SKILL.md. Hex color codes in theme files are wrapped in backtick inline code (e.g., `` `#1a2332` ``), not fenced blocks.

**Lists vs prose ratio:** High list density. SKILL.md uses numbered lists for both Usage Instructions (4 steps) and Application Process (4 steps), plus a bulleted list for Themes Available (10 items) and bullet sub-points under Purpose and Theme Details. Prose paragraphs appear only in the intro paragraph and the Create your Own Theme section.

**Conditional logic:** One implicit conditional in "Create your Own Theme" — triggered only when none of the 10 preset themes fit. Phrasing: "To handle cases where none of the existing themes work for an artifact."

**Templates:** No template syntax (no `{{variables}}`, no placeholder blocks).

**Examples:** No worked examples in SKILL.md. The theme files themselves serve as concrete reference data rather than narrative examples.

**Constraints sections:** No dedicated "Constraints" heading. One hard behavioral constraint embedded inline at line 21: "Do not make any modifications to it; simply show the file for viewing" (referring to `theme-showcase.pdf`).

**Binary asset dependency:** `theme-showcase.pdf` at 124,310 bytes is the largest file in the skill. The skill workflow depends on displaying this PDF to the user before theme selection — making it a required runtime asset, not optional documentation.

**Separation of concern:** SKILL.md contains only workflow logic and theme enumeration. All theme specification data (colors, fonts, use cases) is fully externalized into the 10 individual theme files. This is clean progressive disclosure: SKILL.md stays concise, details are loaded on demand per selected theme.
