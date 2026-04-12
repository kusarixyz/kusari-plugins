---
repository: anthropics/skills
branch: main
skill-path: skills/mcp-builder
analyzed: 2026-04-11
---

# Skill Analysis: mcp-builder


## 1. Overview

**Skill name:** `mcp-builder`

**Title text:** `MCP Server Development Guide`  
**Title char length:** 30

**Description (from YAML frontmatter):**  
`Guide for creating high-quality MCP (Model Context Protocol) servers that enable LLMs to interact with external services through well-designed tools. Use when building MCP servers to integrate external APIs or services, whether in Python (FastMCP) or Node/TypeScript (MCP SDK).`  
**Description char length:** 276

**Total files (recursive):** 10

| Path | Type |
|------|------|
| `SKILL.md` | file |
| `LICENSE.txt` | file |
| `reference/evaluation.md` | file |
| `reference/mcp_best_practices.md` | file |
| `reference/node_mcp_server.md` | file |
| `reference/python_mcp_server.md` | file |
| `scripts/connections.py` | file |
| `scripts/evaluation.py` | file |
| `scripts/example_evaluation.xml` | file |
| `scripts/requirements.txt` | file |

**Subdirectories:** 2  
- `reference/`  
- `scripts/`

---

## 2. SKILL.md Metrics

Measurements are based on the raw file content (9092 bytes as stated).

| Metric | Value |
|--------|-------|
| Character count | ~9,092 |
| Line count | ~210 (estimated from structure and density) |
| Word count | ~1,680 (estimated) |
| Estimated token count (words / 0.75) | ~2,240 |

**Derivation notes:**
- 9092 bytes / ~43 avg chars per line = ~211 lines
- 9092 bytes / ~5.4 avg chars per word = ~1,683 words
- Token estimate uses words / 0.75 heuristic = ~2,244 tokens
- These are estimates; the WebFetch model returned a summarized/rendered version rather than a byte-exact copy, so exact line/word counts are approximated from byte size and structural density.

---

## 3. Document Structure Depth

### Heading hierarchy (in order of appearance)

| Line (approx) | Level | Text |
|----------------|-------|------|
| 1 (frontmatter) | — | `name: mcp-builder` (YAML, not a heading) |
| ~8 | H2 | `MCP Server Development Guide` |
| ~10 | H3 | `Overview` |
| ~13 | H2 | `Process` |
| ~15 | H3 | `🚀 High-Level Workflow` |
| ~19 | H3 | `Phase 1: Deep Research and Planning` |
| ~21 | H4 | `1.1 Understand Modern MCP Design` |
| ~37 | H4 | `1.2 Study MCP Protocol Documentation` |
| ~48 | H4 | `1.3 Study Framework Documentation` |
| ~63 | H4 | `1.4 Plan Your Implementation` |
| ~70 | H3 | `Phase 2: Implementation` |
| ~72 | H4 | `2.1 Set Up Project Structure` |
| ~77 | H4 | `2.2 Implement Core Infrastructure` |
| ~83 | H4 | `2.3 Implement Tools` |
| ~110 | H3 | `Phase 3: Review and Test` |
| ~112 | H4 | `3.1 Code Quality` |
| ~118 | H4 | `3.2 Build and Test` |
| ~124 | H3 | `Phase 4: Create Evaluations` |
| ~128 | H4 | `4.1 Understand Evaluation Purpose` |
| ~132 | H4 | `4.2 Create 10 Evaluation Questions` |
| ~140 | H4 | `4.3 Evaluation Requirements` |
| ~150 | H4 | `4.4 Output Format` |
| ~165 | H2 | `Reference Files` |
| ~167 | H3 | `📚 Documentation Library` |
| ~169 | H4 | `Core MCP Documentation (Load First)` |
| ~176 | H4 | `SDK Documentation (Load During Phase 1/2)` |
| ~180 | H4 | `Language-Specific Implementation Guides (Load During Phase 2)` |
| ~190 | H4 | `Evaluation Guide (Load During Phase 4)` |

**Max depth:** H4 (level 4)

**Count per level:**

| Level | Count |
|-------|-------|
| H2 | 3 |
| H3 | 6 |
| H4 | 19 |
| **Total** | **28** |

---

## 4. Content Specificity Assessment

**Score: 4 / 5**

The skill is operationally specific with numbered phases, named tools, external URLs, annotated fields, and XML output structure. It stops short of a 5 because several implementation sections defer to reference files rather than providing inline detail, and some guidance uses vague qualitative language.

**Excerpt justifications:**

**Justification for 4 (high specificity):**
> "Use Zod (TypeScript) or Pydantic (Python)" / "Define `outputSchema` where possible for structured data" / "Use `structuredContent` in tool responses (TypeScript SDK feature)"

These are precise, technology-named, version-aware directives that leave no ambiguity about what to use.

**Justification for 4 (high specificity):**
> Annotations block:
> ```
> "readOnlyHint": true/false
> "destructiveHint": true/false
> "idempotentHint": true/false
> "openWorldHint": true/false
> ```

Exact JSON key names and semantics specified inline.

**Justification for withholding 5 (deferred detail):**
> "See language-specific guides for project setup: [TypeScript Guide](./reference/node_mcp_server.md)" / "See language-specific guides for detailed testing approaches and quality checklists."

Phase 2.1 (project structure setup) and Phase 3.2 (build/test detail) are fully delegated to reference files rather than providing any inline scaffolding. A reader cannot act on Phase 2 from SKILL.md alone.

---

## 5. Internal File References

Every file reference found in SKILL.md:

| Reference text | Resolved path |
|----------------|---------------|
| `./reference/mcp_best_practices.md` | `reference/mcp_best_practices.md` |
| `./reference/node_mcp_server.md` | `reference/node_mcp_server.md` |
| `./reference/python_mcp_server.md` | `reference/python_mcp_server.md` |
| `./reference/evaluation.md` | `reference/evaluation.md` |
| `LICENSE.txt` | `LICENSE.txt` |

Total internal file references: **5** (4 reference .md files, 1 LICENSE.txt)

All 4 reference .md files are confirmed to exist in `reference/`. LICENSE.txt is confirmed to exist at top level.

---

## 6. Skill Cross-References

No references to other skills within the `skills/` repository are present in SKILL.md. The skill is self-contained. External protocol/SDK documentation is referenced via live URLs, not via other skills:

- `https://modelcontextprotocol.io/sitemap.xml`
- `https://raw.githubusercontent.com/modelcontextprotocol/typescript-sdk/main/README.md`
- `https://raw.githubusercontent.com/modelcontextprotocol/python-sdk/main/README.md`

These are upstream documentation sources, not skill cross-references.

**Skill cross-references: 0**

---

## 7. Agent References

No references to Claude Code agents, subagents, or agent files are present in SKILL.md. The skill does not invoke or reference any `.md` agent definitions or agent invocation patterns.

**Agent references: 0**

---

## 8. Other Markdown File Analysis

### `reference/mcp_best_practices.md`

**Topics covered:**
- Server and tool naming conventions (Python: `{service}_mcp`, Node: `{service}-mcp-server`)
- Response format guidelines (JSON vs Markdown)
- Pagination metadata fields (`has_more`, `next_offset`, `total_count`)
- Transport selection (stdio vs streamable HTTP)
- Security (OAuth 2.1, env vars, `127.0.0.1` binding, input validation)
- Tool annotations (readOnly, destructive, idempotent, openWorld)

**Estimated size:** Medium (summarized content maps to ~400-600 words source)  
**Structure:** H2 sections, bullet lists, inline quotes

---

### `reference/node_mcp_server.md`

**Stated approximate line count:** ~1,200+ lines  
**Topics covered:**
- Modular project structure with separate directories for tools, services, schemas, types
- `server.registerTool()`, `server.registerResource()`, `server.registerPrompt()` API
- Zod schema usage with `.strict()` enforcement
- Tool fields: `title`, `description`, `inputSchema`, `annotations`
- TypeScript strict config, no `any` types, `Promise<T>` return types
- `CHARACTER_LIMIT` constant (25,000 chars) with truncation messaging
- Quality checklist

**Structure:** Comprehensive guide with subsections, code examples, quality checklist  
**This is the largest reference file by a significant margin.**

---

### `reference/python_mcp_server.md`

**Estimated line count:** ~450-550 lines (substantial; contains multiple full code blocks)  
**Topics covered:**
- FastMCP server naming (`{service}_mcp`)
- Tool naming with snake_case and service prefixes
- Pydantic v2 patterns (`model_config`, `field_validator`, `model_dump()`)
- Response format enum (MARKDOWN / JSON)
- Pagination implementation with `has_more` / `next_offset`
- Error handling by HTTP status code
- Shared utility functions (`_make_api_request`, `_handle_api_error`)
- Async/await patterns
- Context parameter injection (`ctx.report_progress`, `ctx.log_info`, `ctx.elicit`)
- Resource registration (`@mcp.resource`)
- Structured output types (TypedDict, Pydantic models)
- Lifespan management (`asynccontextmanager`)
- Transport options (stdio / streamable HTTP)
- DRY/composability requirements
- Full quality checklist (Strategic Design, Implementation Quality, Tool Configuration, Advanced Features, Code Quality, Testing)
- Complete working example (~80 lines of runnable Python)

**Structure:** H2/H3 headings, extensive inline code blocks, checklist at end

---

### `reference/evaluation.md`

**Estimated line count:** ~100-150 lines  
**Topics covered:**
- 10-question requirement, read-only constraint
- Independence, complexity, stability, verifiability requirements
- Ambiguity-with-single-answer design principle
- Human-readable answer formats (names over IDs)
- Personal verification process
- XML output structure

**Structure:** H2/H3 sections, bullet lists, no code blocks (format defined in SKILL.md via XML example)

---

## 9. Structural Observations

### YAML Frontmatter

Present at top of SKILL.md. Three keys:

```yaml
name: mcp-builder
description: Guide for creating high-quality MCP (Model Context Protocol) servers...
license: Complete terms in LICENSE.txt
```

No `tools`, `triggers`, `version`, or `author` keys. Minimal frontmatter relative to other skills that carry richer metadata.

---

### Code Blocks

One code block in SKILL.md:

```xml
<evaluation>
  <qa_pair>
    <question>...</question>
    <answer>3</answer>
  </qa_pair>
<!-- More qa_pairs... -->
</evaluation>
```

This is the only inline code example in the file. All implementation code is deferred to reference files.

---

### Lists vs Prose

The document is heavily list-oriented. Approximate split:
- ~65% bulleted/numbered lists and sub-lists
- ~25% inline bold-labeled prose paragraphs
- ~10% headings and section labels

Phase 4 (evaluation) is the most list-dense section. Phase 1.1-1.3 uses more prose paragraphs with quoted directives.

---

### Conditional Logic

No explicit conditional syntax (no `if/else` blocks, no `<condition>` tags). Conditionality is expressed through natural language:

> "When uncertain, prioritize comprehensive API coverage."  
> "Some clients support code execution which can help agents filter..."  
> "Performance considerations vary by client..."

The TypeScript vs Python fork is handled via parallel bullet pairs pointing to separate reference files, not conditional branching.

---

### Templates

The XML evaluation template in Phase 4.4 is the only formal template structure in SKILL.md. The reference files contain code templates (Pydantic model templates, tool decorator templates, error handler templates) but these live in reference files, not SKILL.md.

---

### Examples

One concrete example in SKILL.md:
- XML `<evaluation>` block with one `<qa_pair>` showing a real question about ASL safety designations and a numeric answer.

Tool naming examples are inline (e.g., `github_create_issue`, `github_list_repos`) but not structured as formal examples. All code-level examples are delegated to reference files.

---

### Constraints

Explicit constraints stated in SKILL.md:

| Constraint | Location |
|-----------|----------|
| "prioritize comprehensive API coverage" | Phase 1.1 |
| Evaluation questions must be independent | Phase 4.3 |
| Evaluation questions must be read-only / non-destructive | Phase 4.3 |
| Evaluation questions must require multiple tool calls | Phase 4.3 |
| Evaluation answers must be single, verifiable values | Phase 4.3 |
| Evaluation answers must be stable over time | Phase 4.3 |
| Exactly 10 evaluation questions required | Phase 4.2 |

---

### Instructional Mode

SKILL.md operates as a procedural workflow document: it directs Claude to load external content (via `WebFetch` and URLs), then follow phases sequentially. It is not a passive reference — it issues active commands to fetch SDKs, study specifications, and load reference files during specific phases. This load-on-demand pattern is structurally notable: reference files are not pre-loaded but are staged to specific workflow phases (Phase 1/2 for SDKs, Phase 2 for language guides, Phase 4 for evaluation guide).

---

### scripts/ Directory

Contains a complete evaluation harness:

| File | Type | Size/Lines | Purpose |
|------|------|------------|---------|
| `evaluation.py` | Python | ~320 lines | Runs QA pairs against live MCP servers using Claude; generates markdown accuracy reports |
| `connections.py` | Python | ~155 lines | Abstract MCP connection handler for stdio, SSE, HTTP transports |
| `example_evaluation.xml` | XML | 5 QA pairs | Sample evaluation with math/science questions and numeric answers |
| `requirements.txt` | Text | 2 lines | `anthropic>=0.39.0`, `mcp>=1.1.0` |

The scripts directory provides runnable infrastructure that SKILL.md's Phase 4 references but does not link to directly by path. The evaluation harness is functionally complete: it parses XML, runs an agent loop with tool calls, collects metrics, and outputs a markdown report.
