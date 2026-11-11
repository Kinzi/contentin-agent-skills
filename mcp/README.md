# MCP client configs for ContentIn

Server URL for every client: `https://mcp.contentin.io/mcp-server` (Streamable HTTP).

Two ways to authenticate:

- **OAuth** (`*.oauth.*`): the client opens the ContentIn sign-in page; you pick the LinkedIn profile the agent may act for and approve. Use this in anything with a browser.
- **API key** (`*.apikey.*`): create a key at app.contentin.io under Profiles, Connections ("Connect AI clients"), and send it in the `X-MCP-Key` header. Use this for n8n, servers and headless runs. Keys start with `cimcp_`, are shown once, up to five per profile. Each key acts for one profile.

The Codex and OpenClaw snippets are Markdown files with the config in a code block, because the Claude plugin directory accepts only Markdown, text, JSON, YAML and images. Copy the block into the file named at its top.

Never commit a real key. Every snippet here reads it from an environment variable, a prompt, or a `<your key>` placeholder you replace locally.

| Client | File location | Snippets | Notes |
|---|---|---|---|
| Claude Code | `.mcp.json` in the project, or `claude mcp add` | `claude-code/` | OAuth: `claude mcp add --transport http contentin https://mcp.contentin.io/mcp-server`, then `/mcp` and Authenticate. Key: add `--header "X-MCP-Key: <your key>"`. |
| Claude.ai and Claude Desktop | Settings, Connectors, Add custom connector | none needed | Paste the URL, leave client id and secret empty, Connect, sign in. The same dialog has a "Request headers" section if you prefer a key. A connector added on claude.ai also appears in Claude Desktop. `claude-desktop/` holds an `mcp-remote` bridge config only for setups that cannot use Connectors. |
| ChatGPT | Settings, Apps, developer mode, create app or connector | none needed | Enter the URL, choose OAuth. |
| Cursor | `.cursor/mcp.json` (project) or `~/.cursor/mcp.json` | `cursor/` | Sign in from the contentin entry in Cursor's MCP settings. Key form: replace `PASTE_YOUR_CONTENTIN_KEY` with a key from app.contentin.io, Profiles, Connections. |
| VS Code | `.vscode/mcp.json` or "MCP: Add Server" | `vscode/` | Key form prompts for the key once and stores it as a secret. |
| Gemini CLI | `~/.gemini/settings.json` | `gemini-cli/` | OAuth: `oauth.enabled: true`, then `/mcp auth contentin` in a session. Key form puts the key in `headers` (Gemini does not expand env vars in headers). |
| OpenClaw | `~/.openclaw/openclaw.json`, block `mcp.servers` | `openclaw/` (JSON5 fragments inside Markdown files) | OAuth: `auth: "oauth"` then `openclaw mcp login contentin`. Key form: replace `PASTE_YOUR_CONTENTIN_KEY` with a key from app.contentin.io, Profiles, Connections. Check with `openclaw mcp doctor contentin --probe`. |
| Codex CLI | `~/.codex/config.toml` | `codex/` (TOML blocks inside Markdown files) | OAuth: `codex mcp login contentin`. Key form uses `env_http_headers`. |
| n8n | MCP Client Tool node | none (UI) | Endpoint = the URL, transport HTTP Streamable, Authentication = Header Auth with name `X-MCP-Key` and your key as the value. Then pick the tools your workflow or AI Agent node may use. |

Setup guide with screenshots: https://contentin.io/linkedin-mcp-server/setup/
