# Local stdio Server Scaffold

stdio transport for local single-client servers. The client launches the server as a subprocess. Communication happens over stdin/stdout with newline-delimited JSON-RPC messages.

**This is for prototypes and personal tools.** Not recommended for distribution. If the user intends to distribute, push toward remote HTTP.

---

## Critical rule: never write to stdout

stdout is the JSON-RPC message channel. Any non-MCP output corrupts the protocol and breaks the server silently.

| Language | Forbidden | Safe alternative |
|---|---|---|
| TypeScript | `console.log()` | `console.error()` |
| Python | `print()` | `print(..., file=sys.stderr)` or `logging.info()` |

Use a logging library that writes to stderr or files.

---

## TypeScript (Official SDK)

### Setup

```bash
mkdir my-mcp-server && cd my-mcp-server
npm init -y
npm install @modelcontextprotocol/sdk zod
npm install -D typescript
```

In `package.json`, set `"type": "module"`.

### Server

```typescript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

const server = new McpServer(
  { name: "my-local-server", version: "1.0.0" },
  { instructions: "Cross-tool guidance goes here." },
);

server.registerTool("list_files", {
  title: "List Files",
  description: "List files in a directory. Path is relative to the configured root.",
  inputSchema: {
    path: z.string().default(".").describe("Directory path relative to root."),
  },
  annotations: { readOnlyHint: true, destructiveHint: false },
}, async ({ path }) => {
  // Implementation here
  return {
    content: [{ type: "text", text: JSON.stringify([], null, 2) }],
  };
});

async function main() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error("MCP server running on stdio");
}

main().catch((error) => {
  console.error("Fatal error:", error);
  process.exit(1);
});
```

### Claude Desktop configuration

Config file location:
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "my-local-server": {
      "command": "node",
      "args": ["/absolute/path/to/dist/index.js"]
    }
  }
}
```

Use absolute paths. Relative paths are unreliable.

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
import sys
import logging
from fastmcp import FastMCP

# Configure logging to stderr
logging.basicConfig(stream=sys.stderr, level=logging.INFO)

mcp = FastMCP(
    "my-local-server",
    instructions="Cross-tool guidance goes here.",
)


@mcp.tool(annotations={"readOnlyHint": True, "destructiveHint": False})
async def list_files(path: str = ".") -> list:
    """List files in a directory. Path is relative to the configured root.

    Args:
        path: Directory path relative to root.
    """
    # Implementation here
    return []


if __name__ == "__main__":
    mcp.run(transport="stdio")
```

### Claude Desktop configuration

```json
{
  "mcpServers": {
    "my-local-server": {
      "command": "uv",
      "args": ["--directory", "/absolute/path/to/my-mcp-server", "run", "server.py"]
    }
  }
}
```

---

## Environment variables

Pass credentials and configuration via the `env` field in the Claude Desktop config:

```json
{
  "mcpServers": {
    "my-server": {
      "command": "node",
      "args": ["/path/to/server.js"],
      "env": {
        "API_KEY": "your-api-key-here"
      }
    }
  }
}
```

On Windows, you may need to explicitly set `APPDATA` in the `env` field if `npx` fails with `${APPDATA}` in paths.

---

## Shutdown handling

The client-initiated shutdown sequence for stdio:

1. Client closes the input stream to the server.
2. Client waits for the server to exit.
3. Client sends SIGTERM if the server does not exit within a reasonable time.
4. Client sends SIGKILL if the server does not exit after SIGTERM.

The server may also initiate shutdown by closing its output stream and exiting.

Handle graceful shutdown in your server:

```typescript
process.on("SIGTERM", () => {
  console.error("Received SIGTERM, shutting down");
  process.exit(0);
});
```

---

## Troubleshooting

**Server not showing up in Claude Desktop:**
1. Restart Claude Desktop completely (quit, not just close window).
2. Check `claude_desktop_config.json` syntax.
3. Ensure file paths are absolute.
4. Check logs: macOS `~/Library/Logs/Claude/mcp*.log`, Windows `%APPDATA%\Claude\logs\mcp*.log`.
5. Run the server manually from terminal to surface errors.

**Tool calls failing silently:**
1. Check Claude Desktop logs.
2. Verify the server runs without errors standalone.
3. Ensure nothing writes to stdout except MCP messages.
