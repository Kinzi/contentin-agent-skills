# Codex CLI: API key

Paste this into `~/.codex/config.toml` (or `.codex/config.toml` in a trusted project) and replace `PASTE_YOUR_CONTENTIN_KEY` with a key from app.contentin.io, Profiles, Connections.

```toml
# ~/.codex/config.toml (or .codex/config.toml in a trusted project)
# Replace PASTE_YOUR_CONTENTIN_KEY with a key from app.contentin.io, Profiles, Connections.
[mcp_servers.contentin]
url = "https://mcp.contentin.io/mcp-server"
http_headers = { "X-MCP-Key" = "PASTE_YOUR_CONTENTIN_KEY" }
```
