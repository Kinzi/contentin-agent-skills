# OpenClaw: API key

Merge this fragment into the `mcp` block of `~/.openclaw/openclaw.json` (JSON5) and replace `PASTE_YOUR_CONTENTIN_KEY` with a key from app.contentin.io, Profiles, Connections. Do not combine it with `auth: "oauth"`.

```json5
// Fragment for ~/.openclaw/openclaw.json (JSON5). Merge into your existing "mcp" block.
// Replace PASTE_YOUR_CONTENTIN_KEY with a key from app.contentin.io, Profiles, Connections.
// Do not set auth: "oauth" together with this header; OpenClaw ignores static headers while OAuth is on.
{
  mcp: {
    servers: {
      contentin: {
        url: "https://mcp.contentin.io/mcp-server",
        transport: "streamable-http",
        headers: { "X-MCP-Key": "PASTE_YOUR_CONTENTIN_KEY" },
        requestTimeoutMs: 120000,
        connectionTimeoutMs: 10000,
        sslVerify: true,
      },
    },
  },
}
```
