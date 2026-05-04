---
name: create-mcp
description: Build MCP servers from use case through deployment. Use when the user wants to build an MCP server, create an MCP integration, wrap an API for Claude, expose tools to an LLM, connect a service to Claude Desktop, make a Claude connector, or discusses anything involving the Model Context Protocol. Interrogates the use case, picks deployment model (remote HTTP or local stdio), selects tool design pattern, picks framework, scaffolds the server, and guides through testing.
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
---

# Build an MCP Server

When this skill is loaded, output exactly this line before any other response:

> KUSARI-MCP

Guide the developer through designing and building an MCP server. MCP servers come in different shapes. Picking the wrong one early causes painful rewrites. Discovery comes before code.

Do not start scaffolding until Phase 1 questions are answered. If the user's opening message already answers them, acknowledge that and skip to the recommendation.

---

## Phase 0: Resume and route

> **Entry:** Skill loaded. **Exit:** Intent extracted, routed to the correct phase.

Check for existing MCP server work in the project before asking anything:

1. **Resume detection.** Search the working directory for `McpServer`, `FastMCP`, `wrangler.toml` with MCP bindings, or `@modelcontextprotocol/sdk` in package.json. If found, summarize what exists and ask the user what phase they are at: extending tools, fixing a bug, adding auth, or testing. Route to the appropriate phase.
2. **Scope assessment.** Read the user's opening message. Extract any answers to Phase 1 questions that are already provided (deployment target, audience, tool count, auth, content types). Mark those questions as answered.
3. **Route.** If all Phase 1 questions are already answered, skip to Phase 2. If partial, proceed to Phase 1 with only the unanswered questions. If the user's message is vague ("build me an MCP server"), proceed to Phase 1 in full.

---

## Phase 1: Interrogate the use case

> **Entry:** No existing MCP server detected, or user starting fresh. **Exit:** All 5 questions answered.

Ask only unanswered questions in one message. Batch them. Do not interrogate one at a time. Adapt wording to what the user has already said.

### 1. What does it connect to?

| Connects to | Direction |
|---|---|
| Cloud API (SaaS, REST, GraphQL) | Remote HTTP server |
| Local process, filesystem, desktop app | Local stdio |
| Hardware, OS-level APIs | Local stdio |
| Nothing external (pure logic) | Either; default to remote |

### 2. Who will use it?

| Audience | Direction |
|---|---|
| Just me / my team | Local stdio is acceptable |
| Anyone who installs it | Remote HTTP (strongly preferred) |
| Broad distribution | Remote HTTP |

### 3. How many distinct actions?

This determines the tool design pattern in Phase 3.

| Count | Pattern |
|---|---|
| Under ~15 | One tool per action |
| 15-30 | Audit for near-duplicates, one-per-action if clean |
| 30+ | Search + execute |

**Push back on tool count.** Before accepting the user's initial list, question whether each tool carries its own weight. Every tool schema consumes context tokens on every turn. Thirty tools with rich schemas can eat 3-5k tokens before the conversation starts. Suggest consolidation of closely related operations. Merge commonly chained calls into single higher-level tools. But always defer to the user's judgment after making the case.

### 4. What auth does the upstream service use?

| Auth type | Approach |
|---|---|
| None / API key | Read from env var, done |
| OAuth 2.0 | Remote server with CIMD auth; see `references/auth-cimd.md` |

### 5. Does the server need to return rich content?

| Content | Approach |
|---|---|
| Text / JSON only | Standard text content blocks |
| Images, audio, diagrams | Use typed content blocks (image, audio); see `references/tool-design.md` |
| Structured typed output | Use outputSchema + structuredContent with text fallback |

---

## Phase 2: Recommend a deployment model

> **Entry:** All Phase 1 questions answered. **Exit:** Deployment model chosen by user, relevant anti-patterns surfaced.

Based on answers, recommend **one** path. Be opinionated.

### Remote streamable-HTTP server (default recommendation)

A hosted service speaking MCP over streamable HTTP. Recommended for anything wrapping a cloud API.

Why it wins:
- Zero install friction for users. They add a URL.
- One deployment serves all users. You control upgrades.
- OAuth flows work properly. The server handles redirects and token storage.
- Works across Claude Desktop, Claude Code, claude.ai, and third-party MCP hosts.

Choose this unless the server must touch the user's local machine.

Fastest deploy: Cloudflare Workers. See `references/cloudflare-workers.md`.
Portable Node/Python: See `references/remote-http-scaffold.md`.

### Local stdio (prototype only)

A script launched via npx/uvx on the user's machine. Acceptable for personal tools and prototypes.

**Not recommended for distribution.** Users need the right runtime installed. No push updates. Fragile across environments. If the user intends to distribute, push toward remote HTTP.

See `references/local-scaffold.md`.

**After choosing a deployment model, surface the relevant anti-patterns from the Anti-Patterns section at the end of this file. Common anti-patterns always apply. Deployment-specific anti-patterns apply only to the chosen path.**

---

## Phase 3: Pick a tool design pattern

> **Entry:** Deployment model chosen. **Exit:** Tool pattern selected, user has confirmed tool list.

**Constraint: push back on tool count.** Every tool schema consumes context tokens on every turn. Before accepting the user's list, question whether each tool carries its own weight. Make the case for consolidation, then defer to the user.

### Pattern A: One tool per action (small surface, default)

When the action space is small (under ~15 operations), give each a dedicated tool with a tight description and schema.

```
create_issue    -- Create a new issue. Params: title, body, labels[]
update_issue    -- Update an existing issue. Params: id, title?, body?, state?
search_issues   -- Search issues by query string. Params: query, limit?
add_comment     -- Add a comment to an issue. Params: issue_id, body
```

Each tool's schema validates inputs precisely. No discovery round-trips.

**Challenge every addition.** Before adding a tool, ask: does this action justify consuming context tokens on every turn? Could it merge with an existing tool? Is it a variant of another tool that differs only by one parameter? If the user cannot articulate a distinct use case where Claude would select this tool over an existing one, it probably should not exist as a separate tool. Make the case for consolidation, but defer to the user.

### Pattern B: Search + execute (large surface)

When wrapping a large API (30+ endpoints), listing every operation floods the context. Expose two tools:

```
search_actions  -- Given a natural-language intent, return matching actions
                   with their IDs, descriptions, and parameter schemas.
execute_action  -- Run an action by ID with a params object.
```

The server holds the full catalog internally. Claude searches, picks, executes. Context stays lean.

### Hybrid

Promote the 3-5 most-used actions to dedicated tools. Keep the long tail behind search/execute.

See `references/tool-design.md` for schema examples, description writing, and annotation requirements.

---

## Phase 4: Pick a framework

> **Entry:** Tool pattern selected. **Exit:** Framework chosen.

| Framework | Language | Use when |
|---|---|---|
| Official TypeScript SDK (`@modelcontextprotocol/sdk`) | TS/JS | Default choice. Best spec coverage, first to get new features. |
| FastMCP 3.x (`fastmcp` on PyPI) | Python | User prefers Python or is wrapping a Python library. Decorator-based, low boilerplate. |

**Do not use FastMCP 1.0** (the frozen version bundled in the official `mcp` Python SDK). Use jlowin's `fastmcp` 3.x from PyPI.

If the user already has a language preference, go with it. Both produce identical wire protocol.

---

## Phase 5: Scaffold and configure

> **Entry:** Framework chosen. **Exit:** Server scaffolded, all tools registered with required annotations.

**Constraint: every tool MUST have `readOnlyHint`, `destructiveHint`, and `title` annotations.** Read and write operations MUST be separate tools. Every parameter MUST have `.describe()`. These are non-negotiable for Anthropic Directory acceptance.

Once deployment model, tool pattern, and framework are settled, scaffold the server.

### Scaffold selection

| Decision | Reference |
|---|---|
| Remote HTTP, TypeScript | `references/remote-http-scaffold.md` |
| Remote HTTP, Python | `references/remote-http-scaffold.md` |
| Remote HTTP, Cloudflare Workers | `references/cloudflare-workers.md` |
| Local stdio, TypeScript | `references/local-scaffold.md` |
| Local stdio, Python | `references/local-scaffold.md` |

### Mandatory for every tool

Apply these requirements from `references/tool-design.md` to every tool registered:

- `readOnlyHint`, `destructiveHint`, and `title` annotations on every tool.
- Read and write operations in **separate** tools. A single tool handling both GET and POST/PUT/DELETE is rejected by the Anthropic Directory.
- Tight parameter schemas with `.describe()` on every parameter. Use enums, regex, min/max, defaults.
- Disambiguating descriptions. Say what the tool does and what it does NOT do.
- Recovery hints in error responses: `"Item not found. Use search_items to find valid IDs."`

### Server-level features

See `references/server-capabilities.md` for details on each.

- **`instructions` field**: Set on the server for cross-tool behavioral guidance. This is where "always call search before get" belongs. Not in individual tool descriptions.
- **Sampling**: Delegate LLM calls to the host instead of shipping your own model client. Check `clientCapabilities.sampling` first.
- **Progress reporting**: For long-running tools, emit progress notifications with `progress`, `total`, and `message`. Check if `progressToken` was provided.
- **Resource templates**: For parameterized data access (e.g., `weather://forecast/{city}/{date}`). Support parameter completion.

### Auth

If OAuth is needed, see `references/auth-cimd.md`. Use CIMD (Client ID Metadata Document), the preferred auth mechanism since spec 2025-11-25.

---

## Phase 6: Test and validate

> **Entry:** Server scaffolded. **Exit:** All three testing layers completed, testing checklist passed.

See `references/testing.md` for the full testing workflow.

Three layers, in order:

1. **Headless JSON-RPC**: Feed raw JSON-RPC messages into the server. Parse responses. Fast iteration for protocol correctness.
2. **MCP Inspector**: Official dev tool. Interactive verification of tools, resources, prompts. Catches capability mismatches and malformed responses.
3. **Real Claude**: Add the server as a custom connector at claude.ai. This catches what unit tests cannot: tool selection accuracy, description ambiguity, parameter inference failures.

Do not skip layer 3. Type checking and test suites verify code correctness, not feature correctness. A tool can pass every unit test and still be unusable because Claude never selects it.

---

## Beyond tools: the other primitives

Tools are one of three server primitives. Most servers start with tools and never need the others. Knowing they exist prevents reinventing them.

| Primitive | Who triggers it | Use when |
|---|---|---|
| **Resources** | Host application (not the LLM) | Exposing docs, files, data as browsable context. Read-only. URI-based. |
| **Prompts** | User (slash command, command palette) | Canned workflows ("/summarize-thread"). Parameterized templates. |

Resources are application-controlled. The host decides how to discover, retrieve, and present them. Each resource has a URI and MIME type. Resource templates support dynamic URIs with parameter completion.

Prompts are user-controlled. They require explicit invocation. Context-aware: they can reference available resources and tools.

See `references/server-capabilities.md` for implementation details.

---

## Anti-patterns

Surface these based on the deployment model chosen in Phase 2. Common anti-patterns apply to both paths. Deployment-specific anti-patterns apply only to the chosen path.

### Common (always surface)

**Tool sprawl.** Do not create one tool per API endpoint. Consolidate commonly chained operations. Merge similar tools that differ by one parameter. Every tool schema consumes tokens on every turn. A server with 30 tools and rich schemas burns 3-5k tokens before the conversation starts.

**Raw API responses.** Do not return unfiltered API payloads. Strip UUIDs, MIME types, and low-level identifiers the LLM cannot act on. Return semantic names and high-signal data. Truncate large result sets with a message: "Showing 10 of 847 results. Refine the query."

**Behavioral instructions in descriptions.** Do not put "always do X", "you must call Y first", or product promotion in tool descriptions. The Anthropic Directory treats this as prompt injection and rejects it. Cross-tool behavioral guidance belongs in the `instructions` field on the server.

**Skipping capability checks.** Before using sampling, roots, or any advanced feature: check `clientCapabilities` after connection. The SDK throws `CapabilityNotSupported` at runtime if the client lacks support. Every capability-dependent code path needs a guard and a working fallback. Different hosts implement different capability subsets. A server tested only against one host will crash on another.

**FastMCP 1.0.** The frozen version bundled in the official `mcp` Python SDK. Use jlowin's `fastmcp` 3.x from PyPI instead. FastMCP 1.0 is stale and will not receive updates.

### Remote HTTP (surface only when remote is chosen)

**Token passthrough.** Never accept a token and forward it to a downstream API. The MCP authorization spec explicitly forbids this. If your server calls another service, exchange the token or use server-own credentials. A token issued for `api.other-service.com` must be rejected even if the signature checks out.

**Wildcard scopes.** Do not define catch-all scopes (`*`, `all`, `full-access`). Do not bundle unrelated privileges into one scope. Broad scopes expand blast radius on token compromise, increase revocation friction, and obscure audit trails. Start with minimal scopes (e.g., `mcp:tools-read`), escalate with targeted challenges.

**Hand-rolling auth or transport.** The SDK ships `mcpAuthMetadataRouter()`, `requireBearerAuth()`, and transport handlers. Use them. Hand-rolling token validation, OAuth flows, or JSON-RPC framing introduces security bugs and falls behind spec changes.

**Uncontrolled DCR.** Dynamic Client Registration is not recommended (use CIMD instead). If DCR is enabled for backward compatibility, restrict to trusted hosts, audit registrations, and apply rate limits. Unauthenticated DCR means anyone can register a client with your authorization server. The confused deputy attack specifically exploits DCR + static client IDs + consent cookies.

**Monolithic servers.** Do not combine database access, file operations, API calls, and email in one server. Each server should have one clear purpose. Isolated failures, independent scaling, clear ownership.

### Local stdio (surface only when local is chosen)

**Local stdio for distribution.** Do not distribute local stdio servers to end users. Users need the right runtime installed. No push updates. Fragile across environments. If the user intends to distribute, push toward remote HTTP. Note that MCPB (bundled local servers with packaged runtime) is the sanctioned way to ship local servers when local execution is required, but this skill does not yet cover MCPB packaging.

---

## Decision matrix

| Scenario | Deployment | Tool pattern |
|---|---|---|
| Wrap a small SaaS API | Remote HTTP | One-per-action |
| Wrap a large SaaS API (50+ endpoints) | Remote HTTP | Search + execute |
| SaaS API + complex auth | Remote HTTP + CIMD | One-per-action |
| Read local filesystem | Local stdio | One-per-action |
| Drive a local desktop app | Local stdio | One-per-action |
| Personal prototype | Local stdio | Whatever is fastest |
| Broad distribution | Remote HTTP | Depends on surface |

---

## Reference files

- `references/tool-design.md` -- tool descriptions, schemas, annotations, return shapes, output size limits (`anthropic/maxResultSizeChars`), error handling, content types
- `references/auth-cimd.md` -- CIMD auth flow, token validation, audience checking, scope design
- `references/remote-http-scaffold.md` -- remote server scaffolds in TypeScript SDK and FastMCP Python
- `references/local-scaffold.md` -- local stdio scaffolds in TypeScript SDK and FastMCP Python
- `references/server-capabilities.md` -- instructions, sampling, progress, resource templates, capability guards
- `references/testing.md` -- headless JSON-RPC, MCP Inspector, real Claude testing
- `references/cloudflare-workers.md` -- Cloudflare Workers deployment scaffold
