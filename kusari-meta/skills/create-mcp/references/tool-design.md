# Tool Design

Tool schemas and descriptions are prompt engineering. They land directly in the LLM's context and determine whether the model picks the right tool with the right arguments. Most MCP integration bugs trace to vague descriptions or loose schemas.

---

## Descriptions

The description is the contract. It is the only thing Claude reads before deciding whether to call the tool. Write it like a one-line manpage entry plus disambiguating hints.

### Good

```
search_issues -- Search issues by keyword across title and body. Returns up
to `limit` results ranked by recency. Does NOT search comments or PRs;
use search_comments / search_prs for those.
```

Says what it does. Says what it returns. Says what it does NOT do.

### Bad

```
search_issues -- Searches for issues.
```

Claude will call this for anything vaguely search-shaped, including things it cannot handle.

### Disambiguate siblings

When two tools are similar, each description should say when to use the other one:

```
get_user      -- Fetch a user by ID. If you only have an email, use find_user_by_email.
find_user_by_email -- Look up a user by email address. Returns null if not found.
```

---

## Parameter schemas

Tight schemas prevent bad calls. Every constraint expressed in the schema is one fewer thing that can go wrong at runtime.

| Instead of | Use |
|---|---|
| `z.string()` for an ID | `z.string().regex(/^usr_[a-z0-9]{12}$/)` |
| `z.number()` for a limit | `z.number().int().min(1).max(100).default(20)` |
| `z.string()` for a choice | `z.enum(["open", "closed", "all"])` |
| optional with no hint | `.optional().describe("Defaults to the caller's workspace")` |

**Describe every parameter.** The `.describe()` text shows up in the schema Claude sees. Omitting it is leaving precision on the table.

```typescript
{
  query: z.string().describe("Keywords to search for. Supports quoted phrases."),
  status: z.enum(["open", "closed", "all"]).default("open")
    .describe("Filter by status. Use 'all' to include closed items."),
  limit: z.number().int().min(1).max(50).default(10)
    .describe("Max results. Hard cap at 50."),
}
```

---

## Tool annotations

Hints the host uses for UX. Required for Anthropic Directory submission.

| Annotation | Meaning | Host behavior |
|---|---|---|
| `readOnlyHint: true` | No side effects | May auto-approve |
| `destructiveHint: true` | Deletes or overwrites | Confirmation dialog |
| `idempotentHint: true` | Safe to retry | May retry on transient error |
| `openWorldHint: true` | Talks to external APIs | May show network indicator |

Every tool must include `readOnlyHint`, `destructiveHint`, and `title`.

### TypeScript

```typescript
server.registerTool("delete_file", {
  title: "Delete File",
  description: "Permanently delete a file by path.",
  inputSchema: { path: z.string().describe("Absolute file path") },
  annotations: { readOnlyHint: false, destructiveHint: true, idempotentHint: false },
}, handler);
```

### Python

```python
@mcp.tool(annotations={"readOnlyHint": False, "destructiveHint": True, "idempotentHint": False})
async def delete_file(path: str) -> str:
    """Permanently delete a file by path.

    Args:
        path: Absolute file path
    """
    ...
```

---

## Read/write separation

Read and write operations must be in separate tools. A single tool that accepts both GET and POST/PUT/DELETE is rejected by the Anthropic Directory. Documenting safe vs unsafe within one tool's description does not satisfy this requirement.

```
# WRONG: combined
manage_issue -- Create, update, or get an issue depending on params

# CORRECT: separated
get_issue     -- Fetch an issue by ID. readOnlyHint: true
create_issue  -- Create a new issue. destructiveHint: false
update_issue  -- Update an existing issue. destructiveHint: false
delete_issue  -- Delete an issue. destructiveHint: true
```

---

## Return shapes

Claude reads whatever is in `content[].text`. Make it parseable.

**Do:**
- Return JSON for structured data: `JSON.stringify(result, null, 2)`
- Return short confirmations for mutations: `"Created issue #123"`
- Include IDs the LLM will need for follow-up calls
- Truncate huge payloads: `"Showing 10 of 847 results. Refine the query to narrow down."`

**Do not:**
- Return raw HTML
- Return megabytes of unfiltered API response
- Return bare success with no identifier (`"ok"` after a create)

---

## Output size limits (Claude Code)

Claude Code caps each MCP tool result at **25,000 tokens by default**. Results over the cap are truncated before Claude sees them. Two escape hatches exist:

| Mechanism | Where it lives | Use when |
|---|---|---|
| `_meta["anthropic/maxResultSizeChars"]` | Tool registration, server-side | Shipped servers that legitimately need larger payloads |
| `MAX_MCP_OUTPUT_TOKENS` | User env var, client-side | Ad-hoc local tuning; not portable |

The hard ceiling is **500,000 characters** regardless of which mechanism raises the cap. Declare the opt-in on the tool so every client honors it without user configuration:

```typescript
server.registerTool("search_tweets", {
  title: "Search Tweets",
  description: "...",
  inputSchema: { ... },
  annotations: { readOnlyHint: true, destructiveHint: false },
  _meta: { "anthropic/maxResultSizeChars": 500_000 },
}, handler);
```

### Budget below the declared ceiling

The declared value is the host's limit on the full tool result, including the JSON-RPC wrapper. Size the handler's payload budget below it, not at it. For a 500,000 ceiling, a 450,000 byte budget on the content leaves headroom for the envelope, error fields, and any structured output.

### Pair the cap with a continuation contract

Raising the ceiling is not a substitute for pagination. When the payload would exceed the budget, return partial results plus a continuation hint the LLM can act on:

```json
{
  "items": [...],
  "hasMore": true,
  "fetchedTotal": 412,
  "droppedForSize": 87,
  "nextCall": { "since": "...", "until": "..." },
  "hint": "Covered 2026-01-01 to 2026-01-14. 87 tweets dropped for size. Call again with nextCall to continue."
}
```

This is the same principle as the truncation line in **Return shapes** above, but with an explicit next-step payload so Claude does not have to guess continuation parameters.

---

## Error handling

Return MCP tool errors, not exceptions that crash the transport. Include enough detail for Claude to recover or retry differently.

```typescript
if (!item) {
  return {
    isError: true,
    content: [{
      type: "text",
      text: `Item ${id} not found. Use search_items to find valid IDs.`,
    }],
  };
}
```

The recovery hint ("use search_items") turns a dead end into a next step. Classify errors by type:

| Category | Guidance in error |
|---|---|
| Not found | Suggest a search/discovery tool |
| Validation | Show the expected format with an example |
| Permission | State what permission is needed |
| Rate limit | Include retry_after if available |
| Transient | Suggest retry |

---

## Content types beyond text

Tools can return more than strings.

| Type | Shape | Use for |
|---|---|---|
| `text` | `{ type: "text", text: string }` | Default |
| `image` | `{ type: "image", data: base64, mimeType: string }` | Screenshots, charts, diagrams |
| `audio` | `{ type: "audio", data: base64, mimeType: string }` | TTS output, recordings |
| `resource_link` | `{ type: "resource_link", uri, name?, description? }` | Pointer; client fetches later |
| `resource` | `{ type: "resource", resource: { uri, text, mimeType } }` | Inline the full content |

Use `resource_link` for large payloads or when the client might not need it. Embed when it is small and always needed.

---

## Structured output

The spec supports typed output via `outputSchema` + `structuredContent`. Clients can validate the shape.

```typescript
server.registerTool("get_weather", {
  title: "Get Weather",
  description: "Get current weather for a city.",
  inputSchema: { city: z.string() },
  outputSchema: { temp: z.number(), conditions: z.string() },
  annotations: { readOnlyHint: true, destructiveHint: false },
}, async ({ city }) => {
  const data = await fetchWeather(city);
  return {
    content: [{ type: "text", text: JSON.stringify(data) }],
    structuredContent: data,
  };
});
```

Always include the text fallback alongside `structuredContent`. Not all hosts read structured output yet.

---

## Tool count guidance

| Tool count | Guidance |
|---|---|
| 1-15 | One tool per action. Sweet spot. |
| 15-30 | Still workable. Audit for near-duplicates that could merge. |
| 30+ | Switch to search + execute. Optionally promote the top 3-5 to dedicated tools. |

The ceiling is not a hard protocol limit. It is context-window economics. Every tool schema is tokens the LLM spends every turn. Tool names must be 64 characters or fewer.
