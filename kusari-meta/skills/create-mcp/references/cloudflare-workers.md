# Cloudflare Workers Deployment

Fastest path from zero to a live MCP server URL. Cloudflare Workers run at the edge with no infrastructure setup. Uses `McpAgent` from the `agents` package with Durable Objects for session state.

---

## Setup

```bash
npm create cloudflare@latest my-mcp-server -- --template=cloudflare/ai/demos/mcp-server-template
cd my-mcp-server
npm install
```

This scaffolds a Workers project with MCP support pre-configured.

---

## Server structure

```typescript
import { McpAgent } from "agents/mcp";
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { z } from "zod";

export class MyMcpServer extends McpAgent {
  server = new McpServer(
    { name: "my-server", version: "1.0.0" },
    { instructions: "Cross-tool guidance here." },
  );

  async init() {
    this.server.registerTool("example_tool", {
      title: "Example Tool",
      description: "Does a specific thing.",
      inputSchema: {
        query: z.string().describe("Search query"),
      },
      annotations: { readOnlyHint: true, destructiveHint: false },
    }, async ({ query }) => {
      return {
        content: [{ type: "text", text: JSON.stringify({ results: [] }) }],
      };
    });
  }
}

export default {
  fetch(request: Request, env: Env, ctx: ExecutionContext) {
    const url = new URL(request.url);
    if (url.pathname === "/mcp" || url.pathname === "/mcp/") {
      return MyMcpServer.serveFromDurableObject("/mcp", request, env, ctx);
    }
    return new Response("Not found", { status: 404 });
  },
};
```

---

## wrangler.toml

```toml
name = "my-mcp-server"
main = "src/index.ts"
compatibility_date = "2025-01-01"

[durable_objects]
bindings = [
  { name = "MCP_SERVER", class_name = "MyMcpServer" }
]

[[migrations]]
tag = "v1"
new_classes = ["MyMcpServer"]
```

---

## Deploy

```bash
# Local development
npx wrangler dev

# Deploy to production
npx wrangler deploy
```

After deploy, your MCP server is live at `https://my-mcp-server.<your-subdomain>.workers.dev/mcp`.

---

## Environment variables

Set secrets via wrangler:

```bash
npx wrangler secret put API_KEY
```

Access in your server via `this.env.API_KEY`.

---

## Limitations

- Workers have a 30-second CPU time limit per request (longer for paid plans).
- No persistent filesystem. Use KV, D1, or R2 for storage.
- Durable Objects handle session state automatically.
- WebSocket support is available but the MCP transport uses streamable HTTP.

---

## When to use Workers vs a traditional host

| Use Workers when | Use a traditional host when |
|---|---|
| Wrapping a cloud API | Server needs persistent local state |
| Low latency across regions matters | Long-running computations (>30s) |
| Zero infrastructure management | Complex dependency chains |
| Quick prototype to production | On-premise deployment required |
