# Testing MCP Servers

Three testing layers, in order of speed. Each catches things the previous one cannot.

---

## Layer 1: Headless JSON-RPC

Feed raw JSON-RPC messages into the server. Parse responses. Fast iteration for protocol correctness.

### stdio server

Create a `test.jsonl` file with one JSON-RPC message per line:

```jsonl
{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-11-25","capabilities":{},"clientInfo":{"name":"test","version":"0.1.0"}}}
{"jsonrpc":"2.0","method":"notifications/initialized"}
{"jsonrpc":"2.0","id":2,"method":"tools/list"}
{"jsonrpc":"2.0","id":3,"method":"tools/call","params":{"name":"your_tool","arguments":{"query":"test"}}}
```

Pipe it into the server:

```bash
cat test.jsonl | node dist/index.js
```

Parse the output with `jq` to verify response shapes.

### HTTP server

Use curl:

```bash
# Initialize
curl -X POST http://localhost:3000/mcp \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2025-11-25","capabilities":{},"clientInfo":{"name":"test","version":"0.1.0"}}}'

# List tools (include session ID from init response)
curl -X POST http://localhost:3000/mcp \
  -H "Content-Type: application/json" \
  -H "Accept: application/json, text/event-stream" \
  -H "Mcp-Session-Id: <session-id-from-init>" \
  -H "MCP-Protocol-Version: 2025-11-25" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/list"}'
```

### What this catches

- Malformed JSON-RPC responses
- Missing required fields in tool definitions
- Schema validation errors
- Transport framing issues (especially stdout corruption in stdio)

---

## Layer 2: MCP Inspector

Official interactive dev tool. Connects to your server, shows available tools/resources/prompts, lets you invoke them with real arguments.

```bash
npx @modelcontextprotocol/inspector node dist/index.js
```

For HTTP servers:

```bash
npx @modelcontextprotocol/inspector --url http://localhost:3000/mcp
```

### What this catches

- Capability negotiation mismatches
- Tools that are registered but fail on invocation
- Resource template parameter completion issues
- Progress notification delivery
- Session management problems (HTTP transport)

---

## Layer 3: Real Claude testing

Add the server as a custom connector at claude.ai via Settings > Connectors. For local servers, use a Cloudflare tunnel:

```bash
# Expose local server to the internet
npx cloudflared tunnel --url http://localhost:3000
```

Use the generated URL as the connector endpoint.

Claude identifies itself with `clientInfo.name: "claude-ai"` during initialization.

### What this catches (that layers 1 and 2 cannot)

- **Tool selection accuracy**: Does Claude pick the right tool given ambiguous user intent?
- **Description effectiveness**: Are descriptions disambiguating correctly between similar tools?
- **Parameter inference**: Does Claude populate optional parameters when it should?
- **Error recovery**: When a tool returns an error with a recovery hint, does Claude follow it?
- **Multi-tool workflows**: Does the `instructions` field guide Claude to call tools in the right order?
- **Return shape usefulness**: Can Claude reason over the returned data to answer the user's question?

### Testing checklist

Before considering the server complete:

- [ ] Every tool can be discovered via `tools/list`
- [ ] Every tool can be invoked with valid arguments
- [ ] Every tool returns meaningful errors for invalid arguments (not stack traces)
- [ ] Error messages include recovery hints (suggest another tool or correct format)
- [ ] Claude selects the right tool for unambiguous requests
- [ ] Claude does not select the wrong tool for ambiguous requests
- [ ] `instructions` field guidance is followed by Claude
- [ ] Read-only tools are annotated `readOnlyHint: true`
- [ ] Destructive tools are annotated `destructiveHint: true`
- [ ] Every tool has a `title` annotation
- [ ] The server degrades gracefully when optional capabilities are absent
