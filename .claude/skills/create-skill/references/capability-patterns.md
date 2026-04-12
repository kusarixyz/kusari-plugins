# Capability Skill Structural Patterns

Derived from analysis of 17 skills in anthropics/skills (docx, pdf, pptx, xlsx, claude-api, algorithmic-art, canvas-design, brand-guidelines, frontend-design, internal-comms, mcp-builder, slack-gif-creator, theme-factory, web-artifacts-builder, webapp-testing, skill-creator, doc-coauthoring).

## Standard Section Order

A capability skill typically follows this section sequence. Not every section is required -- include only what the domain needs.

1. **Title (H1)** -- short, descriptive. 10-50 characters.
2. **Overview / Quick Reference** (H2) -- routing table or task-to-section map. Lets the model jump to the relevant section without reading the whole file.
3. **Core workflow sections** (H2 each) -- one per major task type. For file-format skills, this is typically: Reading, Creating, Editing. For API skills: Setup, Core Operations, Advanced Features.
4. **Design / Style guidance** (H2) -- when the skill produces visual or formatted output. Color palettes, typography, layout rules.
5. **Common Pitfalls / Anti-Patterns** (H2) -- WRONG/CORRECT pairs. Named failure modes with fixes.
6. **Dependencies** (H2) -- tools, libraries, CLI requirements with install commands.
7. **Reference Files** (H2) -- index of references/ files with one-line descriptions if the skill has split content.

## Code Block Conventions

Code blocks are the primary instruction mechanism for capability skills. Conventions observed across high-quality skills:

- **Language-tag every block.** Use `python`, `bash`, `javascript`, `xml`, `ruby`, `yaml` -- not unlabeled blocks.
- **Inline comments as teaching.** The code block teaches through its comments, not through prose before the block. Put the explanation inside the code:
  ```python
  # CRITICAL: use defusedxml, not xml.etree (XXE vulnerability)
  from defusedxml.minidom import parseString
  ```
- **WRONG/CORRECT pairs.** Show the anti-pattern first (labeled `# WRONG` or `# BAD`), then the correct pattern (labeled `# CORRECT` or `# GOOD`). The contrast is more instructive than the correct pattern alone.
- **Runnable examples preferred.** If a code block can be copy-pasted and executed, it is better than a snippet that requires surrounding context.
- **Numeric constants with units.** When the domain has specific units (DXA for DOCX, RGB triplets for colors, pixel coordinates for PDF forms), state the conversion inline: `width: 12240  # 1440 DXA = 1 inch`.

## File Split Patterns

Three architectural patterns for managing content size:

### Monolithic (10/17 Anthropic skills)
Everything in SKILL.md. Works when total content is under ~3,000 tokens. No references/ directory needed.

### Router/Dispatcher (3/17)
SKILL.md is a thin routing layer that identifies the task type and loads the appropriate sub-file.
- internal-comms: routes by communication type to 4 example files
- pdf: routes to forms.md (form filling) or reference.md (advanced features)
- theme-factory: routes to individual theme definition files

Use this pattern when: the skill covers multiple distinct sub-domains that are mutually exclusive per invocation.

### Progressive Disclosure Index (4/17)
SKILL.md contains summary-level Quick Reference content. Full reference material lives in sub-files loaded on demand.
- claude-api: SKILL.md is a compact dispatcher (~5K tokens). 38+ language-specific files load based on detected language.
- pptx: SKILL.md covers reading, design, QA. editing.md and pptxgenjs.md cover the two creation paths.

Use this pattern when: the full reference corpus exceeds ~5,000 tokens but the user only needs one section per invocation.

## Shared Infrastructure

When multiple capability skills need the same scripts (observed: docx/pptx/xlsx share scripts/office/), two options:
1. **Duplicate** -- copy scripts into each skill. Maximizes portability at the cost of maintenance.
2. **Centralize** -- place shared scripts in a common location referenced by all skills. Requires careful path management.

The Anthropic repo chose duplication. The trade-off is explicit: zero coupling, triple the file count.

## Description Field Patterns

Capability skill descriptions follow a consistent formula:

> Use this skill whenever the user wants to [primary action] with [domain]. This includes [list of 5-10 specific sub-tasks]. Also use when [secondary triggers]. Do NOT use for [explicit exclusions].

Strong descriptions from the analysis:
- docx (645 chars): names 12 trigger conditions AND 4 explicit exclusions
- xlsx (843 chars): includes casual phrasing examples ("the xlsx in my downloads") and 5 "Do NOT trigger" conditions
- claude-api (413 chars): uses uppercase TRIGGER/DO NOT TRIGGER markers

Weak descriptions tend to be short (<200 chars) and list only positive triggers with no exclusions.

## Quality Signals for Capability Skills

A capability skill scores 5/5 specificity when:
- Every section contains at least one code block or concrete reference (not just prose guidance)
- Anti-patterns are shown, not just described
- Numeric constants, format strings, and API parameters are copy-pasteable
- No section says "use appropriate X" without defining what appropriate means
- Dependencies are listed with exact install commands

A capability skill scores 4/5 when it has all of the above except it defers some detail to "see reference" without inline examples, or it contains motivational prose that adds no operational content.
