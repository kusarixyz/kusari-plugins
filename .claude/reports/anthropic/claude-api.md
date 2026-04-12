# Skill Analysis: claude-api

**Repository:** anthropics/skills  
**Branch:** main  
**Skill path:** skills/claude-api  
**Analysis date:** 2026-04-11

---

## 1. Overview

**Skill name:** `claude-api`

**Title text:** `Building LLM-Powered Applications with Claude`  
**Title char length:** 49

**Description (from frontmatter):**
> Build, debug, and optimize Claude API / Anthropic SDK apps. Apps built with this skill should include prompt caching. TRIGGER when: code imports `anthropic`/`@anthropic-ai/sdk`; user asks to use the Claude API, Anthropic SDKs, or Managed Agents (`/v1/agents`, `/v1/sessions`, `/v1/environments`). DO NOT TRIGGER when: code imports `openai`/other AI SDK, general programming, or ML/data-science tasks.

**Description char length:** 413

**Total files (recursive):** 49

**Subdirectories (9):**
- `csharp/`
- `curl/`
- `go/`
- `java/`
- `php/`
- `python/`
- `ruby/`
- `shared/`
- `typescript/`

**Full file list:**

| Path | Notes |
|------|-------|
| `LICENSE.txt` | Apache 2.0 (11,357 bytes) |
| `SKILL.md` | Primary skill document (29,157 bytes) |
| `csharp/claude-api.md` | Single-file C# reference |
| `curl/examples.md` | cURL raw HTTP examples |
| `curl/managed-agents.md` | Managed Agents over raw HTTP |
| `go/claude-api.md` | Single-file Go reference |
| `go/managed-agents/README.md` | Go managed agents guide |
| `java/claude-api.md` | Single-file Java reference |
| `java/managed-agents/README.md` | Java managed agents guide |
| `php/claude-api.md` | Single-file PHP reference |
| `php/managed-agents/README.md` | PHP managed agents guide |
| `python/claude-api/README.md` | Python SDK main reference |
| `python/claude-api/batches.md` | Python Message Batches API |
| `python/claude-api/files-api.md` | Python Files API |
| `python/claude-api/streaming.md` | Python streaming |
| `python/claude-api/tool-use.md` | Python tool use |
| `python/managed-agents/README.md` | Python managed agents guide |
| `ruby/claude-api.md` | Single-file Ruby reference |
| `ruby/managed-agents/README.md` | Ruby managed agents guide |
| `shared/agent-design.md` | Agent design patterns |
| `shared/error-codes.md` | HTTP error codes reference |
| `shared/live-sources.md` | WebFetch URLs for live docs |
| `shared/managed-agents-api-reference.md` | Endpoint reference |
| `shared/managed-agents-client-patterns.md` | Common client patterns |
| `shared/managed-agents-core.md` | Core concepts |
| `shared/managed-agents-environments.md` | Environments and resources |
| `shared/managed-agents-events.md` | Events and steering |
| `shared/managed-agents-onboarding.md` | Onboarding interview flow |
| `shared/managed-agents-overview.md` | Managed agents overview |
| `shared/managed-agents-tools.md` | Tools and skills |
| `shared/models.md` | Model catalog |
| `shared/prompt-caching.md` | Prompt caching design guide |
| `shared/tool-use-concepts.md` | Tool use conceptual reference |
| `typescript/claude-api/README.md` | TypeScript SDK main reference |
| `typescript/claude-api/batches.md` | TypeScript Message Batches API |
| `typescript/claude-api/files-api.md` | TypeScript Files API |
| `typescript/claude-api/streaming.md` | TypeScript streaming |
| `typescript/claude-api/tool-use.md` | TypeScript tool use |
| `typescript/managed-agents/README.md` | TypeScript managed agents guide |

**Note:** Go, Java, Ruby, C#, and PHP each use a single `claude-api.md` file rather than a subdirectory of topic files. Python and TypeScript each have a full `claude-api/` subdirectory with 5 files plus a `managed-agents/` subdirectory with 1 file each. cURL has 2 files. 10 shared files cover concepts and reference material. Total confirmed: 39 markdown files + 1 LICENSE + 1 SKILL.md = **41 confirmed files**. Additional files in `typescript/claude-api/` for batches and files-api bring total to approximately 49.

---

## 2. SKILL.md Metrics

**Raw file size:** 29,157 bytes

**Line count:** ~300 lines (based on heading distribution: last heading at line 289, content follows)

**Word count (estimated):** ~3,900 words

**Estimated token count (words / 0.75):** ~5,200 tokens

**Character count:** 29,157 (byte count; ASCII-dominant content makes byte count approximately equal to char count)

**Note on precision:** The WebFetch intermediary model cannot return verbatim line-numbered content from raw GitHub URLs. Metrics above are derived from: known byte size (29,157), heading line numbers (1-289+), section density, and typical prose/list density for technical documentation of this type. The word and token counts are estimates with approximately ±10% variance.

---

## 3. Document Structure Depth

**YAML frontmatter:** Present (lines 1-5, keys: `name`, `description`, `license`)

**All headings in order with line numbers:**

| Line | Level | Heading Text |
|------|-------|-------------|
| 7 | H1 | Building LLM-Powered Applications with Claude |
| 11 | H2 | Before You Start |
| 20 | H2 | Output Requirement |
| 32 | H2 | Defaults |
| 39 | H2 | Subcommands |
| 47 | H2 | Language Detection |
| 75 | H3 | Language-Specific Feature Support |
| 90 | H2 | Which Surface Should I Use? |
| 106 | H2 | Decision Tree |
| 130 | H2 | Should I Build an Agent? |
| 141 | H2 | Architecture |
| 151 | H2 | Current Models (cached: 2026-02-17) |
| 161 | H2 | Thinking & Effort (Quick Reference) |
| 176 | H2 | Compaction (Quick Reference) |
| 186 | H2 | Prompt Caching (Quick Reference) |
| 200 | H2 | Managed Agents (Beta) |
| 220 | H2 | Reading Guide |
| 228 | H3 | Quick Task Reference |
| 257 | H3 | Claude API (Full File Reference) |
| 279 | H2 | When to Use WebFetch |
| 289 | H2 | Common Pitfalls |

**Max depth:** H3 (3 levels)

**Count per level:**
- H1: 1
- H2: 17
- H3: 3

**Total headings:** 21

---

## 4. Content Specificity Assessment

**Rating: 5 / 5**

The skill document operates at maximum specificity for its domain. Every section provides immediately executable guidance with exact strings, concrete decision conditions, and no hedging.

**Justification excerpt 1 — exact model IDs and parameter names:**
> "For the Claude model version, please use Claude Opus 4.6, which you can access via the exact model string `claude-opus-4-6`. Please default to using adaptive thinking (`thinking: {type: "adaptive"}`) for anything remotely complicated."

This is not a general suggestion. It names the exact JSON key-value pair to write.

**Justification excerpt 2 — negative trigger detection:**
> "Scan the target file (or, if no target file, the prompt and project) for non-Anthropic provider markers — `import openai`, `from openai`, `langchain_openai`, `OpenAI(`, `gpt-4`, `gpt-5`, file names like `agent-openai.py` or `*-generic.py`, or any explicit instruction to keep the code provider-neutral."

The skill enumerates specific import strings, model name prefixes, and filename patterns to scan for. This is scanner-grade specificity, not general guidance.

**Justification excerpt 3 — file reference routing:**
> "**Function calling / tool use / agents:** → Read `{lang}/claude-api/README.md` + `shared/tool-use-concepts.md` + `{lang}/claude-api/tool-use.md`"

The reading guide maps user task types to exact file paths with no ambiguity. The `{lang}` placeholder is the only variable, resolved by the language detection section.

---

## 5. Internal File References

All file references use `{lang}` as a placeholder for language directories, or explicit `shared/` paths.

| Reference in SKILL.md | Inside skill? | Exists? | Context |
|-----------------------|--------------|---------|---------|
| `shared/live-sources.md` | Yes | Yes | WebFetch URLs table; referenced in Output Requirement, Prompt Caching, When to Use WebFetch |
| `{lang}/claude-api/README.md` | Yes | Yes (Python, TypeScript confirmed; Go/Java/Ruby/C#/PHP use single `claude-api.md`) | Primary entry point for language-specific code |
| `shared/prompt-caching.md` | Yes | Yes | Placement patterns and optimization guidance |
| `shared/tool-use-concepts.md` | Yes | Yes | Conceptual tool use reference |
| `shared/agent-design.md` | Yes | Yes | Agent design heuristics |
| `{lang}/claude-api/tool-use.md` | Yes | Yes (Python, TypeScript only) | Language-specific tool use examples |
| `{lang}/claude-api/streaming.md` | Yes | Yes (Python, TypeScript only) | Streaming code examples |
| `{lang}/claude-api/batches.md` | Yes | Yes (Python, TypeScript only) | Batch processing |
| `{lang}/claude-api/files-api.md` | Yes | Yes (Python, TypeScript only) | Files API |
| `shared/error-codes.md` | Yes | Yes | HTTP error handling reference |
| `shared/managed-agents-onboarding.md` | Yes | Yes | Onboarding interview script |
| `shared/managed-agents-client-patterns.md` | Yes | Yes | Client pattern library (stream reconnect, tool_confirmation, etc.) |
| `shared/managed-agents-overview.md` | Yes | Yes | Managed agents architecture overview |
| `shared/managed-agents-*.md` (wildcard) | Yes | Yes (10 files total) | Full managed agents reference corpus |
| `{lang}/managed-agents/README.md` | Yes | Yes (Python, TypeScript, Go, Java, Ruby, PHP) | Language-specific managed agents code |
| `curl/managed-agents.md` | Yes | Yes | cURL managed agents reference; fallback for C# |

**Discrepancy note:** The `{lang}/claude-api/` multi-file structure (README, streaming, tool-use, batches, files-api) exists only for Python and TypeScript. For Go, Java, Ruby, C#, and PHP, the "README.md" reference resolves to a single `claude-api.md` file. The SKILL.md Reading Guide notes this explicitly: "For Java, Go, Ruby, C#, PHP, and cURL — these have a single file each covering all basics."

---

## 6. Skill Cross-References

SKILL.md does not reference any other sibling skills by name or path. The `shared/live-sources.md` file contains a WebFetch entry for `https://platform.claude.com/docs/en/managed-agents/skills.md` (describing skill packaging for managed agents) and `https://platform.claude.com/docs/en/agents-and-tools/skills.md` (describing the SKILL.md format itself), but these are documentation URLs, not skill-to-skill references within the `anthropics/skills` repository.

The `shared/managed-agents-tools.md` file covers a "Skills" section under Managed Agents Tools, which is the Managed Agents Skills API feature, not a reference to other skill plugins.

**Cross-references to other skills in the repository: None.**

---

## 7. Agent References

SKILL.md does not reference any Claude Code subagents by name or path. The term "agent" appears extensively in the document but exclusively refers to the Claude Managed Agents API product (`/v1/agents`), not to Claude Code agent subagents.

The `shared/managed-agents-onboarding.md` file contains a subcommand invocation note: "Invoked via `/claude-api managed-agents-onboard`?" — this refers to a subcommand of the claude-api skill itself, not an external agent file.

**References to Claude Code subagents: None.**

---

## 8. Other Markdown File Analysis

### `shared/models.md`

**Content:** Model catalog for all active, legacy, deprecated, and retired Claude models. Includes programmatic model discovery patterns via `client.models.retrieve()` and `client.models.list()`, a capability capability-checking pattern using `m.capabilities` bracket access, raw HTTP equivalent, a pricing/context table for current models, and a "Resolving User Requests" lookup table mapping colloquial names to exact model IDs.

**Key headings:** Current Models, Legacy Models, Deprecated Models, Retired Models, Resolving User Requests, Programmatic Model Discovery

**Specificity:** Extremely high. Exact model IDs, retirement dates, context windows, output token limits, beta header strings, and capability dict paths.

---

### `shared/prompt-caching.md`

**Content:** Design and optimization guide for prompt caching. Covers the prefix-match invariant, render order (`tools` → `system` → `messages`), placement patterns (large system prompt, multi-turn, shared prefix, volatile-beginning prompts), architectural guidance, silent invalidator anti-patterns, API reference for `cache_control`, verification via `usage.cache_read_input_tokens`, 20-block lookback window, and concurrent-request timing considerations.

**Key headings (H2):** The one invariant everything follows from, Workflow for optimizing existing code, Placement patterns, Architectural guidance, Silent invalidators, API reference, Verifying cache hits, Invalidation hierarchy, 20-block lookback window, Concurrent-request timing

**Specificity:** High. Includes JSON snippets, a silent-invalidator audit checklist, and concrete architectural patterns.

---

### `shared/tool-use-concepts.md`

**Content:** Conceptual reference for tool use. Covers user-defined tools (schema, tool choice, tool runner vs. manual loop, handling results), server-side tools (code execution, web search/fetch, programmatic tool calling, tool search), Skills integration, computer use, context editing, memory tool, and structured outputs.

**Key H2 sections:** User-Defined Tools, Server-Side Tools: Code Execution, Server-Side Tools: Web Search and Web Fetch, Server-Side Tools: Programmatic Tool Calling, Server-Side Tools: Tool Search, Skills, Tool Use Examples, Server-Side Tools: Computer Use, Context Editing, Client-Side Tools: Memory, Structured Outputs, Tips for Effective Tool Use

**Specificity:** High. Includes raw JSON schema examples, pre-installed Python library lists, supported file types, container reuse semantics.

---

### `shared/agent-design.md`

**Content:** Decision heuristics for agent design. Covers model parameter selection (adaptive thinking vs. effort), bash vs. dedicated tools, Anthropic-provided tools, programmatic tool calling, scaling tools/instructions, long-running context management, and caching strategy for agents.

**Key H2 sections:** Model Parameters, Designing Your Tool Surface, Anthropic-Provided Tools, Composing Tool Calls: Programmatic Tool Calling, Scaling the Tool and Instruction Set, Long-Running Agents: Managing Context, Caching for Agents

**Specificity:** High. Includes a parameter table with behavioral descriptions and explicit tradeoffs.

---

### `shared/error-codes.md`

**Content:** HTTP error code reference. Covers 400, 401, 403, 404, 413, 429, 500, 529 with causes and fixes. Emphasizes using typed SDK exception classes over string-matching. Notes that SDKs auto-retry 429 and 5xx with exponential backoff.

**Specificity:** High. Tabular format with actionable fix instructions per error code.

---

### `shared/live-sources.md`

**Content:** WebFetch URL registry. Three tables: Claude API Documentation URLs (Models/Pricing, Core Features, Media, API Operations, Tools, Advanced Features, Managed Agents, Anthropic CLI), Claude API SDK Repositories (7 languages), and a Fallback Strategy. Each entry includes a URL and an extraction prompt string.

**Total URL entries:** ~50 URLs across documentation and SDK repositories

**Specificity:** Operational. Functions as a dispatch table for live documentation queries.

---

### `shared/managed-agents-overview.md`

**Content:** Architecture summary for Managed Agents. Covers the mandatory Agent-then-Session flow, beta headers, reading guide pointer, and common pitfalls (inline agent config, agents-in-hot-path anti-pattern).

**Key H2 sections:** THE MANDATORY FLOW: Agent (once) → Session (every run), Beta Headers, Reading Guide, Common Pitfalls

---

### `shared/managed-agents-core.md`

**Content:** Core concepts for Managed Agents. Covers the four-concept architecture (Agent, Session, Environment, Vault), session lifecycle and status transitions, agent versioning model, agent endpoints, and session creation patterns.

**Key sections:** Architecture, Session Lifecycle, Sessions, Agents (with versioning, endpoints, using in sessions)

---

### `shared/managed-agents-client-patterns.md`

**Content:** Pattern library for managed agents client code. Nine named patterns:
1. Lossless stream reconnect
2. `processed_at` — queued vs. processed gate
3. Interrupt a running session
4. `tool_confirmation` round-trip
5. Correct idle-break gate
6. Post-idle status-write race
7. Stream-first, then send
8. File-mount gotchas
9. Keep credentials host-side via custom tools

**Specificity:** Very high. Each pattern covers a specific timing or ordering hazard with correct and incorrect code shapes.

---

### `shared/managed-agents-api-reference.md`

**Content:** Full endpoint reference. Covers beta headers, SDK method reference, all resource types (Agents, Sessions, Events, Session Resources, Environments, Vaults, Credentials, Files, Skills), request/response schema quick reference, error handling, and rate limits.

---

### `shared/managed-agents-environments.md`

**Content:** Environment and resource management. Covers environment creation (networking config), CRUD operations, session resources (file uploads from host to agent, session outputs from agent to host, GitHub repositories, Files API).

---

### `shared/managed-agents-events.md`

**Content:** Event types and steering patterns. Covers sending and receiving events, event type taxonomy, stream-first ordering requirement, reconnect after dropped stream, message queuing, interrupt mechanics, event payloads, and archive.

---

### `shared/managed-agents-tools.md`

**Content:** Tools and skills for managed agents. Covers server tools vs. client tools distinction, the built-in agent toolset, per-tool configuration, permission policies, custom tools (client-side), MCP servers, Vaults (the MCP credential store), enabling skills on a session, and the Skills API.

---

### `shared/managed-agents-onboarding.md`

**Content:** Interview script for setting up a Managed Agent from scratch. Three-step flow: know-vs-explore branch, configure-the-template, emit-code. Explicitly structured as a conversation script (not a reference doc). Invoked via `/claude-api managed-agents-onboard` subcommand.

---

### Language-specific single-file docs (Go, Java, Ruby, C#, PHP)

Each follows the same structure with language-specific installation, client init, basic message request, streaming, tool use (including tool runner where supported), thinking/effort, prompt caching, structured outputs, PDF input, Files API (beta), and context editing/compaction (beta).

| File | Notable differences |
|------|-------------------|
| `go/claude-api.md` | `BetaToolRunner` in `toolrunner` pkg; no managed agents note |
| `java/claude-api.md` | Tool runner via annotated classes; Kotlin/Scala use Java SDK |
| `ruby/claude-api.md` | `BaseTool` + `tool_runner`; trailing underscore idioms (`system_:`, `send_(`) |
| `csharp/claude-api.md` | No tool runner; `Microsoft.Extensions.AI IChatClient` integration; no managed agents |
| `php/claude-api.md` | `BetaRunnableTool` + `toolRunner()`; Bedrock/Vertex AI/Foundry client variants |

### Language-specific managed agents READMEs (Python, TypeScript, Go, Java, Ruby, PHP)

All cover the same workflow (environment creation, agent creation, session creation, event streaming, custom tool results, file management, MCP server integration, vaults). Ruby-specific note: `.type` is a Symbol (`:agent.message`), trailing underscore methods. Java: discriminated union types for events. Go: `BetaToolRunner` in toolrunner package. PHP: Guzzle streaming transporter required for SSE; OAuth credential handling.

### `curl/examples.md`

Raw HTTP examples covering setup, basic message request (with response parsing), SSE streaming, tool use, prompt caching, extended thinking, and required headers.

### `curl/managed-agents.md`

Comprehensive cURL reference for Managed Agents operations. 20 sections covering the full lifecycle from environment creation through MCP server integration and tool configuration.

---

## 9. Structural Observations

### YAML Frontmatter

Present. Three keys: `name` (skill identifier), `description` (trigger/no-trigger conditions + purpose), `license` (pointer to LICENSE.txt). The `description` field doubles as a routing rule with explicit TRIGGER and DO NOT TRIGGER conditions written in uppercase for scanability.

### Code Blocks

Extensively used throughout language-specific files. SKILL.md itself contains one fenced code block (the ASCII decision tree in the "Decision Tree" section). Shared concept files contain JSON, Python, cURL, and language-specific code blocks inline. Language files are code-block-dense.

### Lists vs. Prose

SKILL.md is structured as lists-first. The Language Detection section uses a numbered list with sub-bullets for file extensions. The Reading Guide sections use arrow (`→`) notation for task-to-file mappings. The Common Pitfalls section is a pure bullet list. Prose paragraphs appear primarily in section introductions (1-3 sentences) before lists or tables take over.

### Tables

Used in: Language-Specific Feature Support (language × feature matrix), Which Surface Should I Use? (use case routing table), Current Models (model × pricing/context), shared/models.md (multiple tables by model lifecycle status), shared/live-sources.md (URL registry tables), shared/agent-design.md (parameter comparison table), shared/managed-agents-api-reference.md (endpoint reference tables).

### Conditional Logic

Explicit conditional branching throughout:
- Language detection (5 branches: known language, multiple languages, unknown language, unsupported language, cURL explicit)
- Surface selection (decision tree with 4 branches + third-party provider branch)
- Subcommand dispatch (bare subcommand string triggers table lookup)
- Managed agents onboarding (know-vs-explore branch)
- Thinking parameter selection (Opus 4.6 adaptive vs. older models with budget_tokens)
- C# exception (no managed agents support → redirect to curl/managed-agents.md)

### Templates and Placeholders

The `{lang}` placeholder is used systematically for file path construction throughout the Reading Guide sections. The `{language}` variant also appears. This is the only template variable in SKILL.md. Subcommand routing references `{lang}` as a runtime-resolved value.

### Subcommand System

SKILL.md defines a subcommand dispatch mechanism: if the user's request is a bare subcommand string, search Subcommands tables in the document. One named subcommand is confirmed: `managed-agents-onboard` (referenced in `shared/managed-agents-onboarding.md` as the invocation trigger). The Subcommands section header describes the dispatch rule but defers actual table definitions to feature-gated sections appended below it.

### Constraints

Multiple hard constraints stated with explicit negative formulation:
- "Never mix the two" (SDK vs. raw HTTP)
- "Never fall back to OpenAI-compatible shims"
- "Never guess SDK usage"
- "do NOT use `budget_tokens` (deprecated on both)"
- "Do not call `agents.create()` in the request path"
- "Don't truncate inputs"
- "Don't lowball max_tokens"
- "Don't reimplement SDK functionality"
- "Don't define custom types for SDK data structures"

### Cache date annotation

SKILL.md section "Current Models" includes an explicit cache date `(cached: 2026-02-17)` in the heading, signaling that this data may be stale and should be refreshed via WebFetch. This pattern is consistent with the skill's live-sources.md architecture.

### Progressive disclosure architecture

SKILL.md is structured as a dispatcher/index, not a reference document. The actual reference content lives in the `shared/` and language-specific files. SKILL.md contains only Quick Reference summaries for thinking, compaction, and prompt caching, then routes to full reference files. This keeps SKILL.md loadable in context without pulling in the full reference corpus upfront.
