# Remote HTTP Server Scaffold

Streamable HTTP is the recommended transport for anything wrapping a cloud API. The server operates as an independent HTTP process handling multiple client connections.

---

## TypeScript (Official SDK)

### Setup

```bash
mkdir my-mcp-server && cd my-mcp-server
npm init -y
npm install @modelcontextprotocol/sdk zod express cors
npm install -D typescript @types/express @types/cors
```

In `package.json`, set `"type": "module"`.

In `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "Node16",
    "moduleResolution": "Node16",
    "outDir": "./dist",
    "strict": true,
    "esModuleInterop": true
  }
}
```

### Server

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StreamableHTTPServerTransport } from "@modelcontextprotocol/sdk/server/streamableHttp.js";
import { isInitializeRequest } from "@modelcontextprotocol/sdk/types.js";
import express from "express";
import cors from "cors";
import { randomUUID } from "node:crypto";
import { z } from "zod";

const app = express();
app.use(express.json());
app.use(cors({
  origin: true,  // validate in production
  exposedHeaders: ["Mcp-Session-Id"],
}));

// Track active sessions
const transports: Record<string, StreamableHTTPServerTransport> = {};

function createServer(): McpServer {
  const server = new McpServer(
    { name: "my-server", version: "1.0.0" },
    { instructions: "Cross-tool guidance goes here. Not in individual descriptions." },
  );

  // Register tools here
  server.registerTool("example_tool", {
    title: "Example Tool",
    description: "Does a specific thing. Does NOT do some other thing; use other_tool for that.",
    inputSchema: {
      query: z.string().describe("Search query. Supports quoted phrases."),
      limit: z.number().int().min(1).max(50).default(10).describe("Max results."),
    },
    annotations: { readOnlyHint: true, destructiveHint: false },
  }, async ({ query, limit }) => {
    // Implementation here
    return {
      content: [{ type: "text", text: JSON.stringify({ results: [] }, null, 2) }],
    };
  });

  return server;
}

// MCP endpoint: POST for client-to-server messages
app.post("/mcp", async (req, res) => {
  const sessionId = req.headers["mcp-session-id"] as string | undefined;
  let transport: StreamableHTTPServerTransport;

  if (sessionId && transports[sessionId]) {
    // Existing session
    transport = transports[sessionId];
  } else if (!sessionId && isInitializeRequest(req.body)) {
    // New session
    transport = new StreamableHTTPServerTransport({
      sessionIdGenerator: () => randomUUID(),
      onsessioninitialized: (sid) => { transports[sid] = transport; },
    });
    transport.onclose = () => {
      if (transport.sessionId) delete transports[transport.sessionId];
    };
    const server = createServer();
    await server.connect(transport);
  } else {
    res.status(400).json({
      jsonrpc: "2.0",
      error: { code: -32000, message: "Bad Request: No valid session ID" },
      id: null,
    });
    return;
  }

  await transport.handleRequest(req, res, req.body);
});

// MCP endpoint: GET for server-initiated SSE stream
app.get("/mcp", async (req, res) => {
  const sessionId = req.headers["mcp-session-id"] as string | undefined;
  if (!sessionId || !transports[sessionId]) {
    res.status(400).send("Invalid or missing session ID");
    return;
  }
  await transports[sessionId].handleRequest(req, res);
});

// MCP endpoint: DELETE for session termination
app.delete("/mcp", async (req, res) => {
  const sessionId = req.headers["mcp-session-id"] as string | undefined;
  if (!sessionId || !transports[sessionId]) {
    res.status(400).send("Invalid or missing session ID");
    return;
  }
  await transports[sessionId].handleRequest(req, res);
});

const PORT = process.env.PORT ?? 3000;
app.listen(PORT, () => {
  console.error(`MCP server running on http://localhost:${PORT}/mcp`);
});
```

---

## Python (FastMCP 3.x)

### Setup

```bash
mkdir my-mcp-server && cd my-mcp-server
uv init
uv add fastmcp
```

### Server

```python
from fastmcp import FastMCP

mcp = FastMCP(
    "my-server",
    instructions="Cross-tool guidance goes here. Not in individual descriptions.",
)


@mcp.tool(annotations={"readOnlyHint": True, "destructiveHint": False})
async def example_tool(query: str, limit: int = 10) -> dict:
    """Does a specific thing. Does NOT do some other thing; use other_tool for that.

    Args:
        query: Search query. Supports quoted phrases.
        limit: Max results. Hard cap at 50.
    """
    # Implementation here
    return {"results": []}


if __name__ == "__main__":
    mcp.run(transport="streamable-http", host="0.0.0.0", port=3000)
```

---

## Security requirements for remote servers

### Origin validation

Servers must validate the `Origin` header on all incoming connections. This prevents DNS rebinding attacks. Invalid origin must return HTTP 403 Forbidden.

### HTTPS

Enforce HTTPS in production. Accept plain HTTP only for `localhost` / `127.0.0.1` during development.

### Local development binding

When running locally, bind to `127.0.0.1`, not `0.0.0.0`. This prevents exposure to the local network.

### Session management

- Session IDs must be globally unique and cryptographically secure (UUID or equivalent).
- Session ID must contain only visible ASCII characters (0x21 to 0x7E).
- Client must include `Mcp-Session-Id` on all requests after initialization.
- Server may terminate sessions at any time; respond with 404 Not Found.
- Client receiving 404 must start a new session.
- Include `MCP-Protocol-Version` header on all requests after initialization.

### CORS

For browser-based clients, expose the `Mcp-Session-Id` header:

```typescript
app.use(cors({
  origin: true,  // restrict to known origins in production
  exposedHeaders: ["Mcp-Session-Id"],
}));
```
