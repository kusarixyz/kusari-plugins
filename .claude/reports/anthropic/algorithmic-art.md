# algorithmic-art

## 1. Overview

**Skill name (directory):** algorithmic-art
**Skill title text:** No H1 heading present in SKILL.md. The document begins with YAML frontmatter followed by prose. The `name` field in frontmatter is `algorithmic-art` (18 characters).

**Skill description (from YAML frontmatter `description:` field):**
> Creating algorithmic art using p5.js with seeded randomness and interactive parameter exploration. Use this when users request creating art using code, generative art, algorithmic art, flow fields, or particle systems. Create original algorithmic art rather than copying existing artists' work to avoid copyright violations.

Character length: 329 characters.

**Total number of files (recursive):** 4
- `LICENSE.txt`
- `SKILL.md`
- `templates/generator_template.js`
- `templates/viewer.html`

**Total number of subdirectories:** 1 (`templates/`)

**All files with relative paths:**
```
LICENSE.txt
SKILL.md
templates/generator_template.js
templates/viewer.html
```

---

## 2. SKILL.md Metrics

- **Line count:** 404
- **Word count:** 2763
- **Estimated token count:** 3684 (2763 / 0.75, rounded)
- **Character count:** 19769

---

## 3. Document Structure Depth

No H1 heading exists in SKILL.md. The document uses H2 as the top level, with H3 as the second level. Maximum heading depth reached: H3.

**Heading count per level:**
- H1: 0
- H2: 9
- H3: 10
- H4: 0
- H5: 0
- H6: 0

**Headline breakdown (level, line number, text):**

| Level | Line | Text |
|-------|------|------|
| H2 | 15 | ALGORITHMIC PHILOSOPHY CREATION |
| H3 | 23 | THE CRITICAL UNDERSTANDING |
| H3 | 34 | HOW TO GENERATE AN ALGORITHMIC PHILOSOPHY |
| H3 | 54 | PHILOSOPHY EXAMPLES |
| H3 | 78 | ESSENTIAL PRINCIPLES |
| H2 | 90 | DEDUCING THE CONCEPTUAL SEED |
| H2 | 101 | P5.JS IMPLEMENTATION |
| H3 | 105 | STEP 0: READ THE TEMPLATE FIRST |
| H3 | 133 | TECHNICAL REQUIREMENTS |
| H3 | 201 | CRAFTSMANSHIP REQUIREMENTS |
| H3 | 211 | OUTPUT FORMAT |
| H2 | 221 | INTERACTIVE ARTIFACT CREATION |
| H3 | 227 | CRITICAL: WHAT'S FIXED VS VARIABLE |
| H3 | 259 | REQUIRED FEATURES |
| H3 | 338 | USING THE ARTIFACT |
| H2 | 347 | VARIATIONS & EXPLORATION |
| H2 | 359 | THE CREATIVE PROCESS |
| H2 | 386 | RESOURCES |
| H3 | (within RESOURCES) | (no additional H3 under RESOURCES) |

**Total headings:** 18 (0 H1, 9 H2, 9 H3)

Note: The H3 heading at line 105 contains emoji/warning characters in the original: `⚠️ STEP 0: READ THE TEMPLATE FIRST ⚠️`.

---

## 4. Content Specificity Assessment

**Rating: 4** — Mostly specific, actionable instructions with some framing.

The skill contains a minority of philosophical/framing content (the philosophy creation section and "essential principles") but the majority is directive: exact step sequences, explicit "do this / do not do that" rules, specific template usage mandates, and precise UI structure requirements. Code block examples are illustrative rather than copy-paste production code, but the structural constraints are granular and enforceable.

**Representative excerpts:**

1. Line 105-108 (explicit read-before-write mandate):
   > "CRITICAL: BEFORE writing any HTML: 1. Read `templates/viewer.html` using the Read tool. 2. Study the exact structure, styling, and Anthropic branding. 3. Use that file as the LITERAL STARTING POINT"

2. Lines 133-136 (exact code pattern required):
   > "ALWAYS use a seed for reproducibility" followed by the exact `randomSeed(seed); noiseSeed(seed);` pattern marked as mandatory.

3. Lines 227-258 (fixed vs. variable UI structure):
   > The FIXED/VARIABLE breakdown enumerates by name which sidebar sections must be preserved verbatim (seed display, prev/next/random/jump buttons, regenerate/reset/download buttons) versus which sections the implementer customizes (algorithm, parameter sliders, colors section).

The framing sections ("Algorithmic Philosophy Creation," "Deducing the Conceptual Seed") are higher-level and qualitative, which prevents a rating of 5. The operative implementation sections are highly specific.

---

## 5. Internal File References

Two files are referenced from SKILL.md, both internal to the skill directory.

| Reference as written | Inside skill dir? | File exists? | Context / Section |
|---|---|---|---|
| `templates/viewer.html` | Yes | Yes (20844 bytes) | Referenced in STEP 0 (line ~105) as the mandatory starting point for all HTML artifacts; also referenced throughout the INTERACTIVE ARTIFACT CREATION section and the RESOURCES section |
| `templates/generator_template.js` | Yes | Yes (7826 bytes) | Referenced in the RESOURCES section as a reference for p5.js best practices and code structure; explicitly marked as "NOT a pattern menu" |

No markdown-style hyperlinks (`[text](url)`) exist in the document. References are inline mentions by file path.

---

## 6. Skill Cross-References

None. SKILL.md contains no references to other skills by name or path. No conditional triggers pointing to external skills are present.

---

## 7. Agent References

None. SKILL.md contains no references to named agents, no agent launch directives, and no conditional agent invocations.

---

## 8. Other Markdown File Analysis

There are no `.md` files in the skill directory other than `SKILL.md`. The two non-SKILL.md files are `.js` and `.html`.

**templates/generator_template.js**
- Line count: 222
- Word count: 853
- Estimated token count: 1137 (853 / 0.75, rounded)
- Character count: 7826
- Content: A heavily commented JavaScript file demonstrating p5.js best practices for parameter organization, seeded randomness, class structure, and draw loop patterns. It is explicitly framed as structural guidance, not a generative pattern to copy.
- Referenced from SKILL.md: Yes, in the RESOURCES section as a reference for code structure principles.

**templates/viewer.html**
- Line count: 598
- Word count: 1341
- Estimated token count: 1788 (1341 / 0.75, rounded)
- Character count: 20844
- Content: A complete self-contained HTML file implementing the Anthropic-branded generative art viewer UI, including the p5.js CDN import, sidebar layout with seed controls and action buttons, and a placeholder flow-field algorithm. Serves as the mandatory structural starting point for all output artifacts.
- Referenced from SKILL.md: Yes, extensively. Described as the "REQUIRED STARTING POINT" in the RESOURCES section and mandated for reading via the Read tool before any HTML is written (STEP 0 section).

---

## 9. Structural Observations

**YAML frontmatter fields present:**
- `name`: `algorithmic-art`
- `description`: 329-character usage trigger description
- `license`: `Complete terms in LICENSE.txt` (reference only, not inline text)

**Code blocks:** 5 total
- 3 JavaScript blocks: seeded randomness pattern, params object structure, canvas setup scaffold
- 2 HTML blocks: single artifact structure skeleton, sidebar control-group template snippet

**Use of lists vs. prose:** Heavy use of both. Bulleted lists are used for enumeration of principles, fixed/variable sections, and requirements. Prose is used for the philosophy creation guidance and conceptual framing sections. The ratio is approximately 40% list, 60% prose by line count.

**Use of conditional logic:** Moderate. The "If the philosophy is about X, consider using Y" pattern appears explicitly in the TECHNICAL REQUIREMENTS section (lines ~183-200), providing three conditional branches (organic emergence / mathematical beauty / controlled chaos) with corresponding algorithmic strategies.

**Use of templates and placeholder variables:** High. The document's entire artifact creation workflow is built around two template files. The params object pattern uses inline comments as placeholders (e.g., `// Add parameters that control YOUR algorithm`). The sidebar structure uses `...` as placeholder values in min/max/step/value attributes.

**Use of examples:** The PHILOSOPHY EXAMPLES section (H3, line 54) contains 5 complete named examples ("Organic Turbulence," "Quantum Harmonics," "Recursive Whispers," "Field Dynamics," "Stochastic Crystallization"), each with a one-line philosophy and a paragraph-length algorithmic expression description.

**Constraints/rules sections:** Multiple. The document includes:
- A "CRITICAL GUIDELINES" subsection under HOW TO GENERATE AN ALGORITHMIC PHILOSOPHY with 3 bold-labeled rules
- An "ESSENTIAL PRINCIPLES" H3 section with 6 bulleted constraints
- A "CRAFTSMANSHIP REQUIREMENTS" H3 section with 5 bulleted constraints
- "FIXED" vs. "VARIABLE" delineation under INTERACTIVE ARTIFACT CREATION with explicit lists of what must not be changed
- Repeated "CRITICAL:" inline callouts throughout (at least 6 occurrences)

**Bold emphasis usage:** Extensive. Bold is used for constraint names, section-internal labels, "do not do" lists (marked with ❌), "do" lists (marked with ✅), and inline callout words like "CRITICAL", "REMINDER", "REQUIRED". This creates a dense visual hierarchy within sections that lack subheadings.

**Two-phase workflow structure:** The skill explicitly structures output into a two-step process (philosophy creation → p5.js implementation), with separate major sections and an intermediate "DEDUCING THE CONCEPTUAL SEED" step between them. This pipeline structure is the document's organizing principle.
