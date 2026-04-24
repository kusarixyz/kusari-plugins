# Server Capabilities

Features beyond the three core primitives (tools, resources, prompts). Most are optional. Some are near-free wins.

---

## `instructions` -- system prompt injection

One line of config that lands directly in Claude's system prompt. Use it for cross-tool behavioral hints that do not fit in individual tool descriptions.

### TypeScript

```typescript
const server = new McpServer(
  { name: "my-server", version: "1.0.0" },
  { instructions: "Always call search_items before get_item. IDs are not guessable." },
);
```

### Python

```python
mcp = FastMCP(
    "my-server",
    instructions="Always call search_items before get_item. IDs are not guessable.",
)
```

This is the highest-leverage one-liner in the spec. If Claude keeps misusing your tools, put the fix here. Not in individual tool descriptions (that is treated as prompt injection by the Anthropic Directory).

---

## Sampling -- delegate LLM calls to the host

If your tool logic needs LLM inference (summarize, classify, generate), do not ship your own model client. Ask the host to do it via `sampling/createMessage`. This keeps the server model-independent and avoids API key management.

**Requires client support.** Check `clientCapabilities.sampling` before using.

### TypeScript

```typescript
async (args, extra) => {
  const caps = server.getClientCapabilities();
  if (caps?.sampling) {
    const result = await extra.sendRequest({
      method: "sampling/createMessage",
      params: {
        messages: [{ role: "user", content: { type: "text", text: `Summarize: ${doc}` } }],
        maxTokens: 500,
      },
    }, CreateMessageResultSchema);
    return { content: [{ type: "text", text: result.content.text }] };
  }
  // Fallback: return the raw doc and let Claude handle it
  return { content: [{ type: "text", text: doc }] };
}
```

### Python

```python
@mcp.tool()
async def summarize(ctx: Context, doc: str) -> str:
    """Summarize a document."""
    try:
        response = await ctx.sample("Summarize this document", context=doc)
        return response.text
    except Exception:
        # Fallback: return raw content
        return doc
```

Model preference hints are substring-matched. `"claude-3-5"` matches any Claude 3.5 variant.

---

## Progress reporting -- for long-running tools

When a tool takes more than a few seconds, report progress so the host does not show it as hung. The client sends a `progressToken` in request `_meta`. The server emits progress notifications against it.

### TypeScript

```typescript
async (args, extra) => {
  const token = extra._meta?.progressToken;
  for (let i = 0; i < items.length; i++) {
    if (token !== undefined) {
      await extra.sendNotification({
        method: "notifications/progress",
        params: {
          progressToken: token,
          progress: i,
          total: items.length,
          message: `Processing item ${i + 1} of ${items.length}`,
        },
      });
    }
    await processItem(items[i]);
  }
  return { content: [{ type: "text", text: "Done" }] };
}
```

### Python

```python
@mcp.tool()
async def process_batch(ctx: Context, items: list[str]) -> str:
    """Process a batch of items."""
    for i, item in enumerate(items):
        await ctx.report_progress(progress=i, total=len(items), message=f"Item {i+1}")
        await process_item(item)
    return "Done"
```

Check if `progressToken` was provided before emitting. Not all clients send it. Receiving a progress notification may reset the client's timeout clock, but a maximum timeout should always be enforced.

---

## Resource templates -- parameterized data access

For data that varies by parameters, use resource templates instead of static resources. Templates support dynamic URIs with parameter completion.

### Template definition

```json
{
  "uriTemplate": "weather://forecast/{city}/{date}",
  "name": "weather-forecast",
  "title": "Weather Forecast",
  "description": "Get weather forecast for any city and date",
  "mimeType": "application/json"
}
```

Typing "Par" for `{city}` can suggest "Paris" or "Park City". The system helps discover valid values without requiring exact format knowledge.

### TypeScript

```typescript
server.resource(
  "weather-forecast",
  new ResourceTemplate("weather://forecast/{city}/{date}", {
    list: undefined,
    complete: {
      city: async (partial) => {
        const cities = await searchCities(partial);
        return { values: cities.map(c => c.name) };
      },
    },
  }),
  async (uri, { city, date }) => ({
    contents: [{
      uri: uri.href,
      mimeType: "application/json",
      text: JSON.stringify(await getForecast(city, date)),
    }],
  }),
);
```

---

## Capability check pattern

Every capability-dependent code path needs a guard and a fallback. The SDK throws at runtime if the client lacks support. Do not assume any host supports any optional capability.

```typescript
const caps = server.getClientCapabilities();

// Sampling
if (caps?.sampling) {
  // use sampling
} else {
  // fallback: return raw data, let Claude handle it
}

// Roots (query user-approved directories)
if (caps?.roots) {
  const { roots } = await server.server.listRoots();
  // use roots
} else {
  // fallback: read from env var or config
}
```

Different hosts implement different capability subsets:

| Feature | Server declares | Client must support | Fallback if absent |
|---|---|---|---|
| `instructions` | implicit | always works | n/a |
| Logging | `logging: {}` | always works | stderr |
| Progress | n/a | sends `progressToken` | silently skip |
| Sampling | n/a | `sampling: {}` | return raw data |
| Roots | n/a | `roots: {}` | env var or config |
