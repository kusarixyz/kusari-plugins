# Auth: CIMD (Client ID Metadata Document)

CIMD is the preferred auth mechanism for MCP servers since spec version 2025-11-25. The spec promoted CIMD to SHOULD and demoted Dynamic Client Registration (DCR) to MAY.

---

## When to use auth

Auth is optional. Use it when:

- The server accesses user-specific data (emails, documents, databases)
- You need audit trails for who performed which action
- The upstream API requires user consent
- Enterprise environments with strict access controls
- Rate limiting or usage tracking per user

If the server only reads a static API key from an env var, no OAuth flow is needed.

---

## CIMD flow

The MCP host publishes its client metadata at an HTTPS URL and uses that URL as its `client_id`. Your authorization server fetches the document, validates it, and proceeds with the auth-code flow. No registration endpoint needed. No stored client records.

### Step 1: Initial handshake

Server responds 401 with a pointer to its Protected Resource Metadata:

```http
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer realm="mcp",
  resource_metadata="https://your-server.com/.well-known/oauth-protected-resource"
```

### Step 2: Protected Resource Metadata (PRM) discovery

Client fetches the PRM document (RFC 9728):

```json
{
  "resource": "https://your-server.com/mcp",
  "authorization_servers": ["https://auth.your-server.com"],
  "scopes_supported": ["mcp:tools"]
}
```

### Step 3: Authorization server metadata discovery

Client fetches the auth server's metadata (RFC 8414 or OIDC Discovery):

```json
{
  "issuer": "https://auth.your-server.com",
  "authorization_endpoint": "https://auth.your-server.com/authorize",
  "token_endpoint": "https://auth.your-server.com/token",
  "client_id_metadata_document_supported": true
}
```

The `client_id_metadata_document_supported: true` field tells clients CIMD is available.

### Step 4: Authorization

Client opens a browser to the `/authorize` endpoint. User logs in and grants permissions. Auth server redirects back with an authorization code. Client exchanges code for tokens using OAuth 2.1 Authorization Code with PKCE.

Claude callback URL (all surfaces): `https://claude.ai/api/mcp/auth_callback`

### Step 5: Authenticated requests

Client includes the token in the Authorization header:

```http
POST /mcp HTTP/1.1
Host: your-server.com
Authorization: Bearer eyJhbGciOiJSUzI1NiIs...
```

---

## Token audience validation (required)

Validating "is this token valid" is not enough. The spec requires validating "was this token minted for this server" (RFC 8707 audience). A token issued for `api.other-service.com` must be rejected even if the signature checks out.

### TypeScript

```typescript
const audiences: string[] = Array.isArray(data.aud) ? data.aud : [data.aud];
const allowed = audiences.some((a) =>
  checkResourceAllowed({
    requestedResource: a,
    configuredResource: mcpServerUrl,
  }),
);
if (!allowed) {
  throw new Error(`Audience mismatch. Expected ${mcpServerUrl}, got: ${audiences.join(", ")}`);
}
```

### Python

```python
from mcp.shared.auth_utils import check_resource_allowed, resource_url_from_server_url

resource_url = resource_url_from_server_url(server_url)
aud = token_data.get("aud")
audiences = [aud] if isinstance(aud, str) else (aud or [])
if not any(check_resource_allowed(resource_url, a) for a in audiences):
    return None  # reject
```

---

## SDK auth helpers

The TypeScript SDK ships auth infrastructure. Use it instead of hand-rolling.

**Auth metadata router** (serves the `.well-known/oauth-protected-resource` endpoint):

```typescript
import { mcpAuthMetadataRouter, getOAuthProtectedResourceMetadataUrl }
  from "@modelcontextprotocol/sdk/server/auth/router.js";

app.use(mcpAuthMetadataRouter({
  oauthMetadata,
  resourceServerUrl: mcpServerUrl,
  scopesSupported: ["mcp:tools"],
  resourceName: "My MCP Server",
}));
```

**Bearer auth middleware** (validates tokens on MCP routes):

```typescript
import { requireBearerAuth } from "@modelcontextprotocol/sdk/server/auth/middleware/bearerAuth.js";

const authMiddleware = requireBearerAuth({
  verifier: tokenVerifier,
  requiredScopes: [],
  resourceMetadataUrl: getOAuthProtectedResourceMetadataUrl(mcpServerUrl),
});

app.post("/mcp", authMiddleware, mcpPostHandler);
app.get("/mcp", authMiddleware, handleSessionRequest);
app.delete("/mcp", authMiddleware, handleSessionRequest);
```

---

## Token storage

| Deployment | Store tokens in |
|---|---|
| Remote, stateless | Nowhere. Host sends bearer each request. |
| Remote, stateful | Session store keyed by MCP session ID (Redis, etc.) |
| Local stdio | OS keychain (`keytar` on Node, `keyring` on Python). Never plaintext on disk. |

---

## Scope design

Start with minimal scopes. Do not define catch-all scopes.

| Do | Do not |
|---|---|
| `mcp:tools-read`, `mcp:tools-write` | `*`, `all`, `full-access` |
| Split per capability | Bundle unrelated privileges |
| Escalate with targeted challenges | Grant everything upfront |

---

## What Claude does NOT support

| Auth type | Status |
|---|---|
| CIMD | Supported, recommended |
| DCR | Supported, not recommended |
| `oauth_anthropic_creds` | Partner-only, contact mcp-review@anthropic.com |
| `static_bearer` (user-pasted tokens) | Not supported |
| Pure `client_credentials` (no user consent) | Not supported |

---

## Related standards

- OAuth 2.1 (draft-ietf-oauth-v2-1-13)
- RFC 8414: Authorization Server Metadata
- RFC 9728: Protected Resource Metadata
- RFC 8707: Resource Indicators
