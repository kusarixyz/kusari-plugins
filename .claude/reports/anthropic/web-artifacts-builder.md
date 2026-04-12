# Skill Analysis: web-artifacts-builder

**Repository**: anthropics/skills  
**Branch**: main  
**Skill path**: skills/web-artifacts-builder  
**Analysis date**: 2026-04-11

---

## 1. Overview

**Skill name**: `web-artifacts-builder`

**Title text**: `Web Artifacts Builder`  
**Title character length**: 21

**Description** (from YAML frontmatter):  
`Suite of tools for creating elaborate, multi-component claude.ai HTML artifacts using modern frontend web technologies (React, Tailwind CSS, shadcn/ui). Use for complex artifacts requiring state management, routing, or shadcn/ui components - not for simple single-file HTML/JSX artifacts.`  
**Description character length**: 291

**Total files (recursive)**: 5  
**Subdirectories**: 1 (`scripts/`)

**File list**:

| Path | Type | Approx. Size |
|------|------|-------------|
| `LICENSE.txt` | text | 11,357 bytes |
| `SKILL.md` | markdown | 3,087 bytes |
| `scripts/init-artifact.sh` | bash script | ~7,200 bytes (estimated from content) |
| `scripts/bundle-artifact.sh` | bash script | ~1,800 bytes (estimated from content) |
| `scripts/shadcn-components.tar.gz` | binary archive | 19,500 bytes (19.5 KB) |

---

## 2. SKILL.md Metrics

Measurements derived from the verbatim fetched content (3,087 bytes per task specification).

| Metric | Value |
|--------|-------|
| Line count | 72 |
| Word count | ~470 |
| Estimated token count (words / 0.75) | ~627 |
| Character count | 3,087 |

Notes on methodology:
- Line count: 72 lines total including YAML frontmatter block (5 lines), blank lines, and all body lines.
- Word count: counted from verbatim text; 470 is a close estimate; the YAML frontmatter description alone contributes ~47 words.
- Token estimate uses the standard words/0.75 approximation; actual BPE tokenization would vary.
- Character count: taken from the known byte size (3,087); the file is ASCII-dominant so bytes ≈ characters, minus the 8 Unicode checkmark emoji characters (✅ × 7 occurrences = ~21 extra bytes in UTF-8 vs character count).

---

## 3. Document Structure Depth

**Headings in order with line numbers**:

| Line | Heading text | Level |
|------|-------------|-------|
| 6 | `Web Artifacts Builder` | H1 |
| 18 | `Design & Style Guidelines` | H2 |
| 22 | `Quick Start` | H2 |
| 24 | `Step 1: Initialize Project` | H3 |
| 34 | `Step 2: Develop Your Artifact` | H3 |
| 38 | `Step 3: Bundle to Single HTML File` | H3 |
| 51 | `Step 4: Share Artifact with User` | H3 |
| 55 | `Step 5: Testing/Visualizing the Artifact (Optional)` | H3 |
| 63 | `Reference` | H2 |

**Maximum depth**: H3 (level 3)

**Count per level**:
- H1: 1
- H2: 3 (`Design & Style Guidelines`, `Quick Start`, `Reference`)
- H3: 5 (`Step 1` through `Step 5`)
- H4+: 0

**Total headings**: 9

---

## 4. Content Specificity Assessment

**Rating: 4 / 5**

The skill is highly actionable. Instructions are concrete, commands are runnable verbatim, and decision criteria (when to use vs. not use the skill) are stated explicitly. One point deducted because "Step 2: Develop Your Artifact" defers to a "Common Development Tasks" section that does not exist in SKILL.md — it is either in a missing file or a dead reference.

**Justification excerpts**:

1. High specificity — explicit exclusion criteria in description:
   > `Use for complex artifacts requiring state management, routing, or shadcn/ui components - not for simple single-file HTML/JSX artifacts.`
   This directly tells the model when NOT to invoke the skill, reducing false-positive use.

2. High specificity — exact version pinning with rationale:
   > `Tailwind CSS 3.4.1 with shadcn/ui theming system` and in `init-artifact.sh`: `pnpm install -D tailwindcss@3.4.1`
   The version in the prose matches the script behavior; no ambiguity.

3. Moderate specificity — testing step is under-specified:
   > `use available tools (including other Skills or built-in tools like Playwright or Puppeteer)`
   No specific skill name, command, or tool invocation pattern is given. This is deliberately vague ("optional") but leaves the model to improvise.

---

## 5. Internal File References

All file references found in SKILL.md:

| Reference | Location in document | Type |
|-----------|---------------------|------|
| `scripts/init-artifact.sh` | Step 1 numbered list (line 8) | Script path |
| `scripts/bundle-artifact.sh` | Step 3 numbered list (line 10) | Script path |
| `scripts/init-artifact.sh` | Step 1 bash code block | Script path (repeated) |
| `scripts/bundle-artifact.sh` | Step 3 bash code block | Script path (repeated) |
| `LICENSE.txt` | YAML frontmatter `license` field | License file reference |
| `bundle.html` | Step 3 prose | Output file reference |
| `index.html` | Step 3 requirements note | Required input file reference |
| `.parcelrc` | Step 3 "What the script does" list | Config file reference |

**Total unique file references**: 6 (`scripts/init-artifact.sh`, `scripts/bundle-artifact.sh`, `LICENSE.txt`, `bundle.html`, `index.html`, `.parcelrc`)

**Dead reference**: The phrase "See **Common Development Tasks** below for guidance" in Step 2 references a section that does not exist anywhere in SKILL.md.

---

## 6. Skill Cross-References

**References to other skills in SKILL.md**: 1 (implicit)

- Step 5 mentions "other Skills" generically:
  > `use available tools (including other Skills or built-in tools like Playwright or Puppeteer)`

No specific skill names or skill identifiers are referenced. No `@skill:` syntax or explicit skill URIs present.

---

## 7. Agent References

**References to agents in SKILL.md**: 0

No agent names, agent URIs, or agent invocation patterns appear anywhere in SKILL.md.

---

## 8. Other Markdown File Analysis

**Non-SKILL.md markdown files**: 0

The only markdown file in the skill directory is `SKILL.md`. `LICENSE.txt` is plain text (Apache 2.0, 11,357 bytes), not markdown. No README.md, CHANGELOG.md, or other `.md` files are present.

---

## 9. Structural Observations

### YAML Frontmatter

Present. 4 fields:
```yaml
name: web-artifacts-builder
description: <291-char string>
license: Complete terms in LICENSE.txt
```
(3 key-value pairs between the `---` delimiters; the closing `---` is line 5.)

Fields used: `name`, `description`, `license`.  
Fields absent (compared to typical skill schemas): `version`, `author`, `triggers`, `tools`.

### Code Blocks

2 fenced code blocks in the document body, both typed `bash`:

1. Lines ~27-30: `bash scripts/init-artifact.sh <project-name>` + `cd <project-name>`
2. Lines ~40-42: `bash scripts/bundle-artifact.sh`

Code blocks are minimal — they show invocation commands only, not full script content. All implementation detail lives in the referenced `.sh` files.

### Lists vs Prose

- **Numbered list** (lines 8-12): The 5-step workflow overview at the document top. This is the primary control-flow structure for the model.
- **Bulleted lists with checkmarks** (Step 1 "creates a fully configured project with"): 7 items enumerating what `init-artifact.sh` produces.
- **Bulleted list** (Step 3 "What the script does"): 4 items explaining bundle script behavior.
- **Single-item bulleted list** (Reference section): 1 URL.
- **Prose paragraphs**: Used for step explanations, requirements notes, and the testing caveat. Prose is terse; most sentences are one-clause directives.

Ratio: lists dominate over prose. Approximately 60% of body content is in list form.

### Conditional Logic

1 explicit conditional:
- Step 5 is gated: "Only perform if necessary or requested." Reinforced with: "avoid testing the artifact upfront as it adds latency."

1 implicit conditional in description:
- "not for simple single-file HTML/JSX artifacts" — scopes skill activation.

No `if/else` syntax; conditionals are expressed in natural language.

### Templates

None. No fill-in-the-blank template blocks, variable placeholders (beyond `<project-name>` in the bash invocation), or reusable output templates.

### Examples

No worked examples (no sample App.tsx, no example artifact output, no before/after UI screenshot references). The skill tells the model *how* to run the tools but provides no example of what a finished artifact looks like.

### Constraints

Explicit constraints stated:

1. **Anti-pattern avoidance** (Design & Style section): "avoid using excessive centered layouts, purple gradients, uniform rounded corners, and Inter font." Marked `VERY IMPORTANT`.
2. **Prerequisites for bundling**: Project must have `index.html` in root.
3. **Node version**: Implicit constraint via `init-artifact.sh` — Node 18+ required; script exits with error if below 18.
4. **Testing deferral**: Explicitly constrained — do not test before presenting artifact to user.
5. **Scope constraint** (description): Not for simple single-file artifacts.

### Script Architecture Notes (from `scripts/` analysis)

`init-artifact.sh` (~300 lines):
- OS detection for `sed -i` syntax (macOS vs Linux)
- Node version detection with conditional Vite version pinning (Node 18 → Vite 5.4.11; Node 20+ → latest)
- pnpm installation if absent
- Full Tailwind config, PostCSS config, CSS variables (light + dark mode), tsconfig path aliases, vite.config.ts written inline via heredoc
- 25+ Radix UI packages + 8 additional packages installed
- `shadcn-components.tar.gz` extraction into `src/` — components are pre-built, not fetched from shadcn CLI

`bundle-artifact.sh` (~40 lines):
- Validates `package.json` and `index.html` presence
- Installs `parcel`, `@parcel/config-default`, `parcel-resolver-tspaths`, `html-inline` as dev dependencies
- Creates `.parcelrc` only if not already present
- Cleans `dist/` and `bundle.html` before build
- Outputs a single self-contained `bundle.html`

`shadcn-components.tar.gz` (19.5 KB):
- Binary archive; contains pre-built shadcn/ui component files extracted to `src/`
- Not generated at runtime — shipped with the skill, pinning component versions
