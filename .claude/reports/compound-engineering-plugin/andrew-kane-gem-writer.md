---
repository: EveryInc/compound-engineering-plugin
branch: main
skill-path: plugins/compound-engineering/skills/andrew-kane-gem-writer
analyzed: 2026-04-11
---

# Skill Analysis: andrew-kane-gem-writer


## 1. Overview

**Skill name:** `andrew-kane-gem-writer`

**Title text (from H1 heading):** `Andrew Kane Gem Writer`
**Title char length:** 22 characters

**Description (from YAML frontmatter):**
> This skill should be used when writing Ruby gems following Andrew Kane's proven patterns and philosophy. It applies when creating new Ruby gems, refactoring existing gems, designing gem APIs, or when clean, minimal, production-ready Ruby library code is needed. Triggers on requests like "create a gem", "write a Ruby library", "design a gem API", or mentions of Andrew Kane's style.

**Description char length:** 383 characters

**Total files (recursive):** 6
- `SKILL.md` (top level)
- `references/database-adapters.md`
- `references/module-organization.md`
- `references/rails-integration.md`
- `references/resources.md`
- `references/testing-patterns.md`

**Subdirectories:** 1 (`references/`)

**File list with sizes (from GitHub API):**

| File | Size (bytes) |
|------|-------------|
| SKILL.md | 4,689 |
| references/database-adapters.md | 4,348 |
| references/module-organization.md | 2,250 |
| references/rails-integration.md | 3,792 |
| references/resources.md | 5,382 |
| references/testing-patterns.md | 4,766 |
| **Total** | **25,227** |

---

## 2. SKILL.md Metrics

| Metric | Value |
|--------|-------|
| Character count | 4,689 |
| Line count | ~130 (estimated from content structure) |
| Word count | ~620 (estimated) |
| Estimated token count (words / 0.75) | ~827 tokens |

**Note on line/word counts:** GitHub API provides byte size (4,689) as the authoritative character count. Line and word counts are derived from structural analysis of the retrieved content. The file contains 8 code blocks spanning roughly 70 lines, plus ~60 lines of prose, headings, and list content.

---

## 3. Document Structure Depth

**Headings in order (with line numbers approximate):**

| Line (approx) | Level | Heading Text |
|--------------|-------|-------------|
| 6 | H1 | `Andrew Kane Gem Writer` |
| 10 | H2 | `Core Philosophy` |
| 14 | H2 | `Entry Point Structure` |
| 36 | H2 | `Class Macro DSL Pattern` |
| 57 | H2 | `Rails Integration` |
| 72 | H2 | `Configuration Pattern` |
| 83 | H2 | `Error Handling` |
| 93 | H2 | `Testing (Minitest Only)` |
| 106 | H2 | `Gemspec Pattern` |
| 117 | H2 | `Anti-Patterns to Avoid` |
| 128 | H2 | `Reference Files` |

**Max heading depth:** H2 (depth 2)

**Count per level:**
- H1: 1
- H2: 10
- H3 and below: 0

**Headline breakdown:**
- 1 top-level title
- 10 second-level sections covering: philosophy, entry point, class macros, Rails integration, configuration, error handling, testing, gemspec, anti-patterns, and reference file index

---

## 4. Content Specificity Assessment

**Rating: 5 / 5**

The content is maximally specific. Every section provides executable, production-ready code that can be copied directly. Patterns are named, attributed to specific real gems (Searchkick, PgHero, Strong Migrations, Lockbox, Ahoy), and include both correct and incorrect variations with explicit labeling.

**Excerpt justifications:**

1. **Named anti-patterns with alternatives** (Anti-Patterns section):
   > `method_missing` (use `define_method` instead)
   > Configuration objects (use class accessors)
   > `@@class_variables` (use `class << self`)
   > Committing Gemfile.lock in gems

   This is a closed, exhaustive list of specific Ruby antipatterns. No vague guidance.

2. **WRONG/CORRECT labeling with code** (Rails Integration section):
   ```ruby
   # WRONG
   require "active_record"
   ActiveRecord::Base.include(MyGem::Model)

   # CORRECT
   ActiveSupport.on_load(:active_record) do
     extend GemName::Model
   end
   ```
   Binary contrast with runnable code eliminates interpretation ambiguity.

3. **Explicit require order** (Entry Point Structure):
   The code block labels each require group with numbered comments: `# 1. Dependencies (stdlib preferred)`, `# 2. Internal modules`, `# 3. Conditional Rails (CRITICAL - never require Rails directly)`, `# 4. Module with config and errors`. Order is prescribed, not suggested.

---

## 5. Internal File References

References found in SKILL.md (in the "Reference Files" section):

| Reference | Type |
|-----------|------|
| `references/module-organization.md` | relative file path |
| `references/rails-integration.md` | relative file path |
| `references/database-adapters.md` | relative file path |
| `references/testing-patterns.md` | relative file path |
| `references/resources.md` | relative file path |

All 5 references are to files that exist in the `references/` directory. No broken references. No absolute paths. No references to config files, gemspecs, or external assets.

---

## 6. Skill Cross-References

**None found.**

SKILL.md contains no references to other skills within the plugin or repository. The skill is fully self-contained. The `references/resources.md` file links to external GitHub repositories and blog posts but does not reference other skill modules.

---

## 7. Agent References

**None found.**

SKILL.md contains no references to agents (no `agents/` paths, no agent invocation syntax, no `description:` trigger references pointing to agents). The skill operates as a standalone knowledge module.

---

## 8. Other Markdown File Analysis

### references/module-organization.md

| Metric | Value |
|--------|-------|
| Size | 2,250 bytes |
| Headings | H1: `Module Organization Patterns`; H2s: `Simple Gem Layout`, `Complex Gem Layout (PgHero pattern)`, `Method Decomposition Pattern`, `Version File Pattern`, `Require Order in Entry Point`, `Autoload vs Require`, `Comments Style` |
| H2 count | 7 |
| Code blocks | 8 (directory trees, Ruby modules, require lists) |
| Primary content type | Code-heavy with structural diagrams (ASCII directory trees) |
| Notable content | Explicit `CORRECT` / `AVOID` contrast for `require_relative` vs `autoload`; PgHero `methods/` subdirectory decomposition pattern |

### references/rails-integration.md

| Metric | Value |
|--------|-------|
| Size | 3,792 bytes |
| Headings | H1: `Rails Integration Patterns`; H2s: `The Golden Rule`, `ActiveSupport.on_load Hooks`, `Prepend for Behavior Modification`, `Railtie Pattern`, `Engine Pattern (Mountable Gems)`, `Routes for Engines`, `YAML Configuration with ERB`, `Generator Pattern`, `Conditional Feature Detection` |
| H2 count | 9 |
| Code blocks | 10 (Ruby classes, route DSL, YAML) |
| Primary content type | Code-dominant; each section is primarily a code block with 1-2 lines of prose framing |
| Notable content | Full Railtie and Engine class implementations; conditional Rails version checking; generator template pattern |

### references/database-adapters.md

| Metric | Value |
|--------|-------|
| Size | 4,348 bytes |
| Headings | H1: `Database Adapter Patterns`; H2s: `Abstract Base Class Pattern`, `PostgreSQL Adapter`, `MySQL Adapter`, `MariaDB Adapter (MySQL variant)`, `Adapter Detection Pattern`, `Multi-Database Support (PgHero pattern)`, `Connection Switching`, `SQL Dialect Handling` |
| H2 count | 8 |
| Code blocks | 9 (full adapter class implementations) |
| Primary content type | Almost entirely code; minimal prose |
| Notable content | Full class hierarchy from AbstractAdapter through PostgreSQL/MySQL/MariaDB; regex-based adapter detection using `connection.adapter_name`; PgHero multi-database pattern with `connection_model` using anonymous `Class.new(ActiveRecord::Base)` |

### references/testing-patterns.md

| Metric | Value |
|--------|-------|
| Size | 4,766 bytes |
| Headings | H1: `Testing Patterns`; H2s: `Minitest Setup`, `Test File Structure`, `Multi-Version Testing`, `Rakefile`, `GitHub Actions CI`, `Database-Specific Testing`, `Test Database Setup`, `Assertion Patterns`, `Test Helpers`, `Skipping Tests` |
| H2 count | 10 |
| Code blocks | 12 (Ruby, YAML, Bash) |
| Primary content type | Mixed: YAML for CI config, Ruby for test code, bash for commands |
| Notable content | Full GitHub Actions matrix strategy with Ruby/Rails version combinations; complete `assert_queries` helper using `ActiveSupport::Notifications`; multi-gemfile version testing setup |

### references/resources.md

| Metric | Value |
|--------|-------|
| Size | 5,382 bytes |
| Headings | H1: `Andrew Kane Resources`; H2s: `Primary Documentation`, `Top Ruby Gems by Stars`, `Key Source Files to Study`, `GitHub Profile`, `Blog Posts & Articles`, `Design Philosophy Summary` |
| H2 count | 6 |
| H3 count under `Top Ruby Gems by Stars` | 4 (`Search & Data`, `Database & Migrations`, `Security & Encryption`, `Analytics & ML`, `Utilities`) |
| Code blocks | 0 |
| Primary content type | Tables and bulleted lists; no code |
| Notable content | Markdown tables with star counts for 18+ gems; 30+ direct GitHub URLs to specific source files (not just repo roots); 10-point design philosophy summary; links to ankane.org blog posts |

---

## 9. Structural Observations

### YAML Frontmatter

Present and complete. Fields used:
- `name`: `andrew-kane-gem-writer` (kebab-case, matches directory name)
- `description`: Long-form trigger description (383 chars), written as a skill invocation spec: "This skill should be used when...", "It applies when...", "Triggers on requests like..."

The description follows the pattern of listing concrete invocation conditions rather than summarizing content.

### Code Blocks

SKILL.md contains 8 fenced code blocks. All are `ruby`-tagged except for the `# WRONG` / `# CORRECT` comparison block, which is also Ruby. Reference files add:
- `module-organization.md`: 8 blocks (ruby, plain text for directory trees)
- `rails-integration.md`: 10 blocks (ruby, yaml)
- `database-adapters.md`: 9 blocks (ruby)
- `testing-patterns.md`: 12 blocks (ruby, yaml, bash)
- `resources.md`: 0 blocks

**Total code blocks across skill:** 47

### Lists vs Prose

SKILL.md is prose-light. The only bulleted list is the Anti-Patterns section (8 items) and the Reference Files section (5 items). All other sections use code blocks with inline comments as the primary communication vehicle. Prose exists primarily as 1-3 sentence framing before each code block.

`resources.md` is the exception: it is almost entirely tables and lists with no code.

### Conditional Logic

No conditional logic constructs (if/else, decision trees) appear in the skill prose. Conditional patterns appear only inside Ruby code examples (e.g., `defined?(Rails)`, `if defined?(OpenSearch::Client)`). The skill itself does not contain branching instructions for the model.

### Templates

No fill-in-the-blank templates. The code uses `GemName` and `gemname` as placeholder identifiers throughout all files, functioning as a consistent naming convention rather than a template syntax. This is implicit convention, not explicit template syntax.

### Examples

Every major section in SKILL.md is backed by a complete code example. The Class Macro DSL Pattern section shows both the usage side (calling `searchkick word_start: [:name]`) and the implementation side (the `Module.new` / `define_method` internals) in a single code block. This dual usage+implementation pattern appears in the Rails Integration section as well.

### Constraints

The skill contains several hard constraints stated with imperative language:

- "Every gem follows this exact pattern" (entry point structure)
- "CRITICAL - never require Rails directly" (comment inside code block)
- "WRONG" / "CORRECT" labeled blocks (Rails integration)
- "Minitest Only" (testing section title)
- Anti-Patterns list framed as "to Avoid"
- Gemspec: "NO add_dependency lines" (comment inside code block)

These constraints are embedded in code comments and section framing, not in a dedicated constraints section.

### Cross-File Consistency

The `SKILL.md` references all 5 files in `references/` by explicit path at the bottom. The reference files expand on SKILL.md patterns without contradicting them. `rails-integration.md` repeats the WRONG/CORRECT pattern from SKILL.md verbatim and extends it with 8 additional sections. `database-adapters.md` introduces content not covered in SKILL.md (multi-DB, adapter detection). `resources.md` provides attribution and source verification for the patterns claimed in SKILL.md.
