# OpenClaw: OAuth

Merge this fragment into the `mcp` block of `~/.openclaw/openclaw.json` (JSON5), or use the `openclaw mcp set` command in the comment, then `openclaw mcp login contentin`.

```json5
// Fragment for ~/.openclaw/openclaw.json (JSON5). Merge into your existing "mcp" block,
// or run: openclaw mcp set contentin '{"url":"https://mcp.contentin.io/mcp-server","transport":"streamable-http","auth":"oauth"}'
// then:   openclaw mcp login contentin
{
  mcp: {
    servers: {
      contentin: {
        url: "https://mcp.contentin.io/mcp-server",
        transport: "streamable-http",
        auth: "oauth",
        requestTimeoutMs: 120000,
        connectionTimeoutMs: 10000,
      },
    },
  },
}
```
