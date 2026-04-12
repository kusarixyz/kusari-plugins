# Aggregate Skill Analysis: anthropics/skills

**Repository:** anthropics/skills  
**Branch:** main  
**Skills analyzed:** 17  
**Analysis date:** 2026-04-11

---

## Scale

| Metric | Value |
|--------|-------|
| Total skills | 17 |
| Total files across all skills | ~350+ |
| Total estimated tokens (SKILL.md files only) | ~34,027 |
| Total estimated tokens (all markdown files) | ~50,000+ |

---

## SKILL.md Size Distribution

| Metric | Min | Median | Max |
|--------|-----|--------|-----|
| **Line count** | 32 (internal-comms) | ~210 (mcp-builder) | 590 (docx) |
| **Word count** | ~230 (internal-comms) | ~1,290 (pptx) | ~4,720 (skill-creator) |
| **Token estimate** | ~307 (internal-comms) | ~1,720 (pptx) | ~6,293 (skill-creator) |
| **Character count** | 1,511 (internal-comms) | 8,072 (pdf) | 33,168 (skill-creator) |

### Size tiers

- **Small (<1,000 tokens):** brand-guidelines (375), internal-comms (307), theme-factory (648), web-artifacts-builder (627), webapp-testing (667), frontend-design (680)
- **Medium (1,000-3,000 tokens):** pdf (1,343), slack-gif-creator (1,471), pptx (1,720), mcp-builder (2,240), canvas-design (2,347)
- **Large (3,000+ tokens):** doc-coauthoring (3,147), docx (3,483), algorithmic-art (3,684), xlsx (3,796), claude-api (5,200), skill-creator (6,293)

Six skills are under 1,000 tokens. Six are in the 1,000-3,000 range. Five exceed 3,000. The distribution is bimodal: skills are either compact dispatchers or dense reference documents.

---

## Structure Depth

| Max heading depth | Count | Skills |
|-------------------|-------|--------|
| H2 only | 3 | frontend-design, internal-comms, webapp-testing |
| H3 | 10 | algorithmic-art, brand-guidelines, canvas-design, claude-api, doc-coauthoring, docx, pptx, slack-gif-creator, theme-factory, web-artifacts-builder |
| H4 | 4 | mcp-builder, pdf, skill-creator, xlsx |

**Most common:** H3 (10/17 skills). H4 is used only by the most complex skills. No skill uses H5 or H6.

### Heading counts

| Metric | Min | Median | Max |
|--------|-----|--------|-----|
| Total headings | 2 (frontend-design) | 17 (pptx) | 37 (skill-creator, xlsx) |

### Missing H1

3 skills have no H1 heading in SKILL.md: algorithmic-art, canvas-design, internal-comms. These use the YAML frontmatter `name` field as the sole identifier. The remaining 14 have an explicit H1.

---

## Content Specificity Distribution

| Score | Count | Skills |
|-------|-------|--------|
| 2 (general guidance) | 1 | internal-comms |
| 3 (mixed) | 1 | canvas-design |
| 4 (mostly specific) | 10 | algorithmic-art, brand-guidelines, doc-coauthoring, frontend-design, mcp-builder, pdf, slack-gif-creator, theme-factory, web-artifacts-builder, webapp-testing |
| 5 (extremely granular) | 5 | claude-api, docx, pptx, skill-creator, xlsx |

**Dominant pattern:** 4/5. Most skills provide concrete, actionable instructions. Score-5 skills share a distinguishing trait: they embed exact code, format strings, hex values, or JSON schemas that are directly copy-pasteable. Score-2 (internal-comms) is intentionally a thin dispatcher with all specificity in sub-files.

---

## Cross-Referencing Patterns

### Skill-to-skill references
**0 out of 17 skills reference another skill by name or path.** Every skill is fully self-contained within its directory. The only near-exception is skill-creator, which negatively references `/skill-test` as a prohibited alternative.

### Agent references
**1 out of 17 skills references agents:** skill-creator (3 agents: grader.md, comparator.md, analyzer.md). All other skills have zero agent references. Doc-coauthoring mentions "sub-agents" as a capability check, not named agents.

### Internal file references
**15 out of 17 skills reference at least one internal file.** Only brand-guidelines and canvas-design reference only LICENSE.txt (no operational file references). The typical pattern is referencing scripts via bash invocations or sibling markdown files for deferred content.

### Referencing mechanisms
- **Inline path mentions** (most common): `scripts/recalc.py`, `templates/viewer.html`
- **Markdown links**: `[editing.md](editing.md)` (pptx, pdf)
- **Python import paths**: `from core.gif_builder import GIFBuilder` (slack-gif-creator)
- **Placeholder patterns**: `{lang}/claude-api/README.md` (claude-api)

---

## File Composition

| Metric | Min | Median | Max |
|--------|-----|--------|-----|
| Files per skill | 1 (doc-coauthoring) | 7 (slack-gif-creator) | 83 (canvas-design) |
| Subdirectories | 0 (5 skills) | 1 | 11 (docx) |

### File type breakdown

- **Python scripts** are the dominant non-markdown file type, present in 10/17 skills
- **XSD schemas** inflate file counts for docx (44 XSDs), xlsx (32 XSDs), pptx (shared validators)
- **Binary assets** appear in 3 skills: canvas-design (49 .ttf fonts), theme-factory (1 PDF), web-artifacts-builder (1 .tar.gz)
- **3 skills share the same `scripts/office/` infrastructure:** docx, pptx, xlsx (pack, unpack, validate, soffice)

### Supplementary markdown files

| Has supplementary .md files | Count | Skills |
|-----------------------------|-------|--------|
| Yes | 6 | claude-api (38+), internal-comms (4), mcp-builder (4), pdf (2), pptx (2), skill-creator (4), theme-factory (10) |
| No (SKILL.md only) | 10 | algorithmic-art, brand-guidelines, canvas-design, doc-coauthoring, docx, frontend-design, slack-gif-creator, web-artifacts-builder, webapp-testing, xlsx |

Claude-api is an outlier with 38+ supplementary markdown files across 9 language directories and a shared corpus.

---

## Title and Description Lengths

### Title (H1 or name field)

| Metric | Value |
|--------|-------|
| Min | 4 chars (xlsx) |
| Median | 18 chars |
| Max | 49 chars (claude-api: "Building LLM-Powered Applications with Claude") |

### Description (frontmatter)

| Metric | Value |
|--------|-------|
| Min | 204 chars (webapp-testing) |
| Median | 318 chars (skill-creator) |
| Max | 843 chars (xlsx) |

**1 skill (pptx) has no YAML frontmatter at all** -- no name, description, or license fields. This is the only skill without frontmatter.

Long descriptions (>400 chars) tend to embed explicit trigger/no-trigger conditions. xlsx (843 chars) includes 5 explicit "Do NOT trigger" conditions. claude-api (413 chars) uses uppercase TRIGGER/DO NOT TRIGGER markers.

---

## Structural Conventions

### YAML frontmatter fields

| Field | Prevalence |
|-------|-----------|
| `name` | 16/17 (all except pptx) |
| `description` | 16/17 (all except pptx) |
| `license` | 16/17 (all except pptx) |
| Other fields | 0/17 |

The frontmatter schema is minimal and consistent: exactly 3 fields. No skill uses `version`, `author`, `tools`, `triggers`, or any other field.

### Common heading patterns

Sections that appear across multiple skills:
- **Overview / Quick Reference** -- 7 skills
- **Dependencies** -- 5 skills (docx, pptx, slack-gif-creator, webapp-testing, xlsx)
- **Common Pitfalls / Avoid** -- 5 skills (claude-api, docx, pptx, webapp-testing, xlsx)
- **Best Practices** -- 3 skills (webapp-testing, xlsx, claude-api)
- **Keywords** -- 2 skills (brand-guidelines, internal-comms)
- **Philosophy** -- 2 skills (slack-gif-creator, algorithmic-art via "Essential Principles")

### Content patterns

| Pattern | Count | Notes |
|---------|-------|-------|
| Code blocks present | 14/17 | Only brand-guidelines, canvas-design, and theme-factory have zero fenced code blocks |
| Tables present | 8/17 | brand-guidelines, claude-api, docx, pdf, pptx, skill-creator, webapp-testing, xlsx |
| WRONG/CORRECT anti-pattern pairs | 4/17 | docx, pptx, xlsx, claude-api |
| Explicit prohibitions (NEVER/DO NOT) | 14/17 | Average ~5 prohibitions per skill |
| Conditional branching | 9/17 | doc-coauthoring, pdf/forms.md, claude-api, mcp-builder, skill-creator, internal-comms, web-artifacts-builder, webapp-testing, xlsx |
| Worked examples | 8/17 | algorithmic-art, skill-creator, slack-gif-creator, pptx, docx, pdf, webapp-testing, xlsx |
| Templates or output schemas | 6/17 | skill-creator, mcp-builder, doc-coauthoring, pdf/forms.md, pptx, xlsx |
| Behavioral constraints on agent | 4/17 | docx ("Do not write Python scripts"), slack-gif-creator ("only when asked"), web-artifacts-builder ("avoid testing upfront"), skill-creator ("Do NOT use /skill-test") |

---

## Architectural Patterns

Three distinct structural architectures emerge:

### 1. Monolithic reference (10/17)
SKILL.md contains all instructions. No supplementary markdown. Scripts may exist for tooling.
**Skills:** algorithmic-art, brand-guidelines, canvas-design, doc-coauthoring, docx, frontend-design, slack-gif-creator, web-artifacts-builder, webapp-testing, xlsx

### 2. Router/dispatcher (3/17)
SKILL.md is thin and routes to sub-files based on input type or task.
**Skills:** internal-comms (routes by communication type), pdf (routes to forms.md and reference.md), theme-factory (routes to theme files)

### 3. Progressive disclosure index (4/17)
SKILL.md acts as a compact dispatcher/index with summary-level content. Full reference material loads on demand from sub-files during specific workflow phases.
**Skills:** claude-api (language-specific + shared reference corpus), mcp-builder (phased reference loading), pptx (editing.md + pptxgenjs.md), skill-creator (agents + references + schemas)

---

## Shared Infrastructure

Three skills (docx, pptx, xlsx) share an identical `scripts/office/` directory containing:
- `pack.py`, `unpack.py` -- ZIP-level manipulation of Office Open XML files
- `validate.py` -- XSD schema validation
- `soffice.py` -- LibreOffice headless conversion
- `helpers/` -- merge_runs.py, simplify_redlines.py
- `validators/` -- base.py, docx.py, pptx.py, redlining.py
- `schemas/` -- ISO/IEC 29500, ECMA, MCE, Microsoft extension XSDs

This shared infrastructure is duplicated across all three skill directories rather than centralized. The file contents appear identical.

---

## Observations

1. **No cross-skill dependencies.** Every skill is a standalone unit. This maximizes portability but means shared patterns (anti-pattern rules, Office XML infrastructure) are duplicated.

2. **Frontmatter is used exclusively for routing, not execution control.** No skill uses frontmatter to declare tool permissions, model preferences, or execution constraints. All behavioral control is embedded in the document body.

3. **Description length correlates with trigger precision.** Skills with longer descriptions (xlsx, docx, claude-api) embed explicit negative triggers ("Do NOT trigger when..."). Shorter descriptions rely on positive matching only.

4. **Code-block density predicts specificity score.** All score-5 skills have 10+ code blocks. Score-2 and score-3 skills have 0 code blocks in SKILL.md.

5. **Binary assets are rare but load-bearing.** Only 3/17 skills include binary files, but when present they are required at runtime (fonts for rendering, PDFs for display, tarballs for project scaffolding).

6. **The `scripts/office/` duplication across docx/pptx/xlsx is the largest structural inefficiency** in the repository. 40+ files are replicated three times.

7. **Only skill-creator uses H4 heading depth for instructional content.** The other H4 users (pdf, mcp-builder, xlsx) use it for reference subsections. Skill-creator uses it for its embedded "Skill Writing Guide" -- a meta-layer teaching skill construction.
