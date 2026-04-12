# Skill Analysis: slack-gif-creator

**Repository:** anthropics/skills  
**Branch:** main  
**Skill path:** skills/slack-gif-creator  
**Analysis date:** 2026-04-11

---

## 1. Overview

**Skill name:** slack-gif-creator  
**Title text (YAML `name` field):** `slack-gif-creator` (18 chars)  
**Description:** "Knowledge and utilities for creating animated GIFs optimized for Slack. Provides constraints, validation tools, and animation concepts. Use when users request animated GIFs for Slack like \"make me a GIF of X doing Y for Slack.\""  
**Description character length:** 228 chars  

**Total files (recursive):** 6  
**Subdirectories:** 1 (`core/`)  

**File list:**

| Path | Size (bytes) |
|------|-------------|
| `LICENSE.txt` | 11357 |
| `SKILL.md` | 7841 |
| `requirements.txt` | 66 |
| `core/easing.py` | 6265 |
| `core/frame_composer.py` | 4548 |
| `core/gif_builder.py` | 9847 |
| `core/validators.py` | 3785 |

Total files: 7 (including LICENSE.txt at top level)

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Line count | 254 |
| Word count | 1103 |
| Estimated token count (words / 0.75) | 1471 |
| Character count | 7841 |

---

## 3. Document Structure Depth

**Max depth:** H3 (3 levels)  
**Heading counts by level:** H1: 1, H2: 10, H3: 13  
**Total real markdown headings:** 24

**Headings in order (outside code blocks):**

| Line | Level | Text |
|------|-------|------|
| 7 | H1 | Slack GIF Creator |
| 11 | H2 | Slack Requirements |
| 22 | H2 | Core Workflow |
| 45 | H2 | Drawing Graphics |
| 47 | H3 | Working with User-Uploaded Images |
| 60 | H3 | Drawing from Scratch |
| 84 | H3 | Making Graphics Look Good |
| 111 | H2 | Available Utilities |
| 113 | H3 | GIFBuilder (`core.gif_builder`) |
| 122 | H3 | Validators (`core.validators`) |
| 135 | H3 | Easing Functions (`core.easing`) |
| 150 | H3 | Frame Helpers (`core.frame_composer`) |
| 162 | H2 | Animation Concepts |
| 164 | H3 | Shake/Vibrate |
| 170 | H3 | Pulse/Heartbeat |
| 176 | H3 | Bounce |
| 182 | H3 | Spin/Rotate |
| 187 | H3 | Fade In/Out |
| 194 | H3 | Slide |
| 201 | H3 | Zoom |
| 207 | H3 | Explode/Particle Burst |
| 214 | H2 | Optimization Strategies |
| 234 | H2 | Philosophy |
| 250 | H2 | Dependencies |

Note: Lines 28, 31, 41, 57, 68, 71, 75, 78, 127, 130, 140, 143, 146, 147, 225 contain `#` characters but are Python/bash comments inside fenced code blocks, not markdown headings.

---

## 4. Content Specificity Assessment

**Score: 4 / 5**

The skill is highly specific in its technical prescriptions. It provides exact numeric constraints, named function signatures, import paths, and parameter names. The animation concepts section gives concrete algorithmic approaches rather than vague descriptions. One point withheld because the animation concept sections stop short of full code examples (they are bullet-point pseudocode rather than runnable implementations).

**Justifications:**

1. **Exact Slack constraints with numeric values** (lines 12-18):
   > "Emoji GIFs: 128x128 (recommended) / Message GIFs: 480x480 / FPS: 10-30 / Colors: 48-128 / Duration: Keep under 3 seconds for emoji GIFs"
   
   These are precise, actionable platform requirements, not approximate guidelines.

2. **Named easing variants enumerated** (lines 145-147):
   > `# Available: linear, ease_in, ease_out, ease_in_out, bounce_out, elastic_out, back_out`
   
   All valid string values for the `easing` parameter are listed verbatim, removing ambiguity.

3. **Negative constraints with rationale** (lines 83, 241-243):
   > "Don't use: Emoji fonts (unreliable across platforms) or assume pre-packaged graphics exist in this skill."
   > "It does NOT provide: Rigid animation templates or pre-made functions / Emoji font rendering (unreliable across platforms)"
   
   Explicit exclusions are stated twice with reasons, which prevents common misuse patterns.

---

## 5. Internal File References

All file references found in SKILL.md:

| Line | Reference | Context |
|------|-----------|---------|
| 4 | `LICENSE.txt` | YAML frontmatter `license` field |
| 25 | `core.gif_builder` | `from core.gif_builder import GIFBuilder` (code block) |
| 42 | `output.gif` | `builder.save('output.gif', ...)` (code block) |
| 56 | `file.png` | `Image.open('file.png')` (code block) |
| 113 | `core.gif_builder` | Section heading `### GIFBuilder (\`core.gif_builder\`)` |
| 119 | `out.gif` | `builder.save('out.gif', ...)` (code block) |
| 122 | `core.validators` | Section heading `### Validators (\`core.validators\`)` |
| 125 | `core.validators` | `from core.validators import validate_gif, is_slack_ready` (code block) |
| 128 | `my.gif` | `validate_gif('my.gif', ...)` (code block) |
| 131 | `my.gif` | `is_slack_ready('my.gif')` (code block) |
| 135 | `core.easing` | Section heading `### Easing Functions (\`core.easing\`)` |
| 138 | `core.easing` | `from core.easing import interpolate` (code block) |
| 150 | `core.frame_composer` | Section heading `### Frame Helpers (\`core.frame_composer\`)` |
| 153 | `core.frame_composer` | `from core.frame_composer import (...)` (code block) |
| 227 | `emoji.gif` | `builder.save('emoji.gif', ...)` (code block) |

Module references map directly to actual files in `core/`:
- `core.gif_builder` -> `core/gif_builder.py` (9847 bytes)
- `core.validators` -> `core/validators.py` (3785 bytes)
- `core.easing` -> `core/easing.py` (6265 bytes)
- `core.frame_composer` -> `core/frame_composer.py` (4548 bytes)

---

## 6. Skill Cross-References

None. SKILL.md contains no references to other skills, no `skills/` path mentions, and no inter-skill dependency declarations.

---

## 7. Agent References

None. SKILL.md contains no references to agents, subagents, or agent invocation patterns.

---

## 8. Other Markdown File Analysis

No markdown files other than SKILL.md exist in the skill directory. The `core/` subdirectory contains only `.py` files. `LICENSE.txt` and `requirements.txt` are plain text.

---

## 9. Structural Observations

**YAML Frontmatter**

Present at lines 1-5. Fields:
- `name: slack-gif-creator`
- `description:` (228-char trigger description with example invocation phrase)
- `license: Complete terms in LICENSE.txt`

The description includes a concrete trigger phrase: `"make me a GIF of X doing Y for Slack."` — this is a usage hint aimed at routing, not just a summary.

**Code Blocks**

9 fenced code blocks total:

| Block | Language | Approx lines | Purpose |
|-------|----------|-------------|---------|
| 1 | python | ~20 | Core Workflow full example (GIFBuilder end-to-end) |
| 2 | python | ~4 | Loading user-uploaded image |
| 3 | python | ~19 | PIL ImageDraw primitives reference |
| 4 | python | ~6 | GIFBuilder API |
| 5 | python | ~10 | Validators API |
| 6 | python | ~12 | Easing interpolate API |
| 7 | python | ~9 | Frame Helpers imports |
| 8 | python | ~9 | Maximum optimization example |
| 9 | bash | ~1 | pip install command |

Code blocks account for approximately 90 lines out of 254 total (~35% of the document).

**Lists vs Prose**

The document is heavily list-structured. Every H3 section under "Animation Concepts" uses 3-4 bullet points. The "Philosophy" section uses bullet lists for both what the skill provides and what it does not. The "Optimization Strategies" section uses a numbered list. Prose paragraphs are minimal and appear primarily in "Making Graphics Look Good" (lines 84-110) and the "Philosophy" section.

Rough split: ~55% bullet lists, ~35% code blocks, ~10% prose paragraphs.

**Conditional Logic**

One explicit conditional instruction at line 214: "Only when asked to make the file size smaller, implement a few of the following methods:" — this gates the Optimization Strategies section behind user intent, preventing over-optimization by default.

One branch at lines 47-56 for user-uploaded images: two explicit decision paths ("Use it directly" vs "Use it as inspiration") with PIL code for the load path.

**Templates**

No fill-in-the-blank templates. Code examples use placeholder variable names (`frame`, `builder`, `draw`) but are functional patterns, not templates.

**Examples**

The Core Workflow block (lines 23-43) is a complete end-to-end example covering all three steps: builder instantiation, frame loop, and save call. The Maximum Optimization block (lines 223-231) is a second complete save-call example. The PIL primitives block (lines 62-81) functions as a reference card with four shape type examples.

**Constraints**

Explicit constraints found:
1. Do not use emoji fonts (stated twice: line 83 and line 242)
2. Do not assume pre-packaged graphics exist (line 83)
3. Minimize optimization unless user explicitly requests smaller file size (line 214)
4. `width=2` or higher required for outlines (line 87)
5. Dimensions must match Slack spec: 128x128 for emoji, 480x480 for messages
6. Duration under 3 seconds for emoji GIFs
7. FPS range 10-30
8. Color palette 48-128

The skill uses both positive mandates ("use thicker lines", "use vibrant colors") and negative prohibitions (the "does NOT provide" list), giving the consuming agent a clear behavioral boundary.
