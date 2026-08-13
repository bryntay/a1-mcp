# Installing the A1 Gallery MCP server

This file is for AI agents setting up the A1 MCP server on a user's machine.

## What this is

A remote MCP server at `https://www.a1.gallery/api/mcp`. There is nothing to clone, build
or run locally. No API key, no environment variables, no npm package.

## Steps

1. Add the server to the user's MCP config using the snippet for their client (below).
2. Tell the user to complete the browser sign-in their client opens on first connect.
3. Verify with a `tools/list` — you should see 17 tools, all read-only.

## Config by client

**Claude Code**

```bash
claude mcp add --transport http a1 --scope user https://www.a1.gallery/api/mcp
```

**Codex CLI**

```bash
codex mcp add a1 --url https://www.a1.gallery/api/mcp
```

**Cursor** (`~/.cursor/mcp.json`) and **Claude Desktop**

```json
{
  "mcpServers": {
    "a1": {
      "url": "https://www.a1.gallery/api/mcp"
    }
  }
}
```

**VS Code** (`.vscode/mcp.json`)

```json
{
  "servers": {
    "a1": {
      "type": "http",
      "url": "https://www.a1.gallery/api/mcp"
    }
  }
}
```

**Windsurf** (`~/.codeium/windsurf/mcp_config.json`)

```json
{
  "mcpServers": {
    "a1": {
      "serverUrl": "https://www.a1.gallery/api/mcp"
    }
  }
}
```

**Zed** (`settings.json`)

```json
{
  "context_servers": {
    "a1": {
      "url": "https://www.a1.gallery/api/mcp"
    }
  }
}
```

## Authentication

OAuth 2.1 with PKCE and dynamic client registration. The client handles it — do not try to
mint tokens manually and do not ask the user for credentials.

A free A1 account is required. If the user does not have one, send them to
https://www.a1.gallery/login. Free accounts get 50 tool calls a day.

## Troubleshooting

- **401 on every call** — the user is not signed in. Trigger a reconnect so the client
  reruns the OAuth flow.
- **Server shows zero tools** — the handshake ran unauthenticated. Reconnect and sign in.
- **Rate limited** — the free tier is 50 tool calls a day. It resets at midnight UTC.
