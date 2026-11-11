# ContentIn for Agents: LinkedIn skills for your AI agent

Agent skills and MCP configs that connect Claude, ChatGPT, Claude Code, Cursor, Gemini CLI, OpenClaw, Codex, n8n or any other MCP client to [ContentIn](https://contentin.io/linkedin-for-ai-agents/), so the agent you already run writes LinkedIn posts in your voice from your own material, schedules and publishes them through LinkedIn's official API after you confirm, measures them, and (on Agent Pro) shows you who engaged.

Your agent can already write. On its own it writes like everyone else's agent. Connected to ContentIn it gets your voice and your own stories and numbers (so it stops inventing), what worked on your account, the people who engaged with your posts scored against your ideal customer, and a safe last mile: nothing goes out without your confirmation.

## What is in this repo

| Path | What |
|---|---|
| `skills/contentin-linkedin/SKILL.md` | The main skill: when to use each of the 13 tools, which plan each needs, the capture, voice, draft, confirm, schedule workflow, the confirmation rule, and what to tell the user when a tool refuses. |
| `skills/contentin-linkedin-leads/SKILL.md` | The lead workflow (Agent Pro or Pro): list the people who engaged, pick, draft a reply or note the user sends themselves. Never sends anything. |
| `.claude-plugin/` | Plugin and marketplace manifests, so this repo installs as a Claude Code plugin that brings the MCP server and both skills. |
| `plugin.json`, `mcp.json` | The same plugin in the [Agent Plugins](https://agent-plugins.org) format read by Cursor's plugin directory and OpenAI's plugin tooling. |
| `.mcp.json` | The MCP server in the shape Claude Code and Cursor read from a project root. |
| `gemini-extension.json` | The same package as a Gemini CLI extension: `gemini extensions install https://github.com/Kinzi/contentin-agent-skills`. |
| `mcp/` | Ready config snippets per client, in OAuth form and in API-key form. |

No code. The skills are plain Markdown following the [Agent Skills](https://agentskills.io/specification) standard. The MCP server runs at `https://mcp.contentin.io/mcp-server` (Streamable HTTP).

## Who it is for

People who run AI agents and automations and post on LinkedIn: founders, solo consultants, coaches, fractional executives, and the people who build LinkedIn workflows in n8n or Claude Code for them.

## 1. Get a ContentIn account

Create the account at [app.contentin.io/signup?product=agent](https://app.contentin.io/signup?product=agent&ref=agents_lp), or connect from your AI client and create it on the sign-in page that opens. Paste your LinkedIn profile URL; ContentIn reads your published posts and shows you how you write. Account, connection and voice profile are free, no card.

The tools that read your posts, write, schedule and publish need a plan: **Agent** at $29 or **Agent Pro** at $49 a month per LinkedIn profile, each with a 7-day trial (card required). Already on ContentIn Growth or Pro? The same tools are included (Growth = Agent tools, Pro = Agent Pro tools), nothing to buy.

## 2. Connect the MCP server

Server URL for every client: `https://mcp.contentin.io/mcp-server`

| Client | How |
|---|---|
| **Claude Code** | `claude mcp add --transport http contentin https://mcp.contentin.io/mcp-server` then `/mcp`, select contentin, Authenticate. Or install the plugin (next section). |
| **Claude.ai and Claude Desktop** | Settings, Connectors, Add custom connector. Paste the URL, leave client id and secret empty, Connect, sign in with ContentIn. |
| **ChatGPT** | Settings, Apps, turn on developer mode, create a new app or connector, enter the URL, choose OAuth. |
| **Cursor** | Copy `mcp/cursor/mcp.oauth.json` to `.cursor/mcp.json` (project) or `~/.cursor/mcp.json`, then sign in from the contentin entry in Cursor's MCP settings. |
| **VS Code** | Copy `mcp/vscode/mcp.oauth.json` to `.vscode/mcp.json`, or run "MCP: Add Server" and paste the URL. |
| **Gemini CLI** | `gemini extensions install https://github.com/Kinzi/contentin-agent-skills` (brings the server and both skills), then `/mcp auth contentin`. Or merge `mcp/gemini-cli/settings.oauth.json` into `~/.gemini/settings.json`. |
| **OpenClaw** | `openclaw mcp set contentin '{"url":"https://mcp.contentin.io/mcp-server","transport":"streamable-http","auth":"oauth"}'` then `openclaw mcp login contentin`. Or merge the JSON5 fragment in [`mcp/openclaw/openclaw.oauth.md`](mcp/openclaw/openclaw.oauth.md). |
| **Codex CLI** | Add the TOML block from [`mcp/codex/config.oauth.md`](mcp/codex/config.oauth.md) to `~/.codex/config.toml`, then `codex mcp login contentin`. |
| **n8n and scripts** | Create an API key in ContentIn under Profiles, Connections ("Connect AI clients"). In n8n add an MCP Client node, endpoint = the URL, transport HTTP Streamable, Authentication = Header Auth with name `X-MCP-Key` and the key as value. |

API keys work in every client that accepts headers: send `X-MCP-Key: <your key>`. The `*.apikey.*` files in `mcp/` show the exact shape per client. Each key or OAuth grant is bound to one ContentIn profile, which you pick when you connect. Revoke any time under Profiles, Connections, Connected apps.

Full setup guide: https://contentin.io/linkedin-mcp-server/setup/

## 3. Install the skills

With the [skills CLI](https://skills.sh) (Claude Code, Cursor, Codex, Gemini CLI, OpenClaw, Copilot, Windsurf and others; needs Node.js 22.20+):

```bash
npx skills add Kinzi/contentin-agent-skills
```

Pick one skill only:

```bash
npx skills add Kinzi/contentin-agent-skills --skill contentin-linkedin
```

As a Claude Code plugin (brings the MCP server too):

```bash
claude plugin marketplace add Kinzi/contentin-agent-skills
claude plugin install contentin-linkedin@contentin
```

Then run `/mcp` once to sign in. Other agents: copy the `skills/<name>/` folder into the place your agent reads skills from (for example `.claude/skills/`, `.cursor/skills/`, `.agents/skills/`, or `skills/` in an OpenClaw workspace).

## The 13 tools

| Tool | Plan |
|---|---|
| `get_account_status`: setup, plan, LinkedIn connection and what each tool is waiting for | any connected account |
| `get_voice_context`: your voice, rules, saved material, best posts and strategy, served before the agent writes | Agent |
| `list_posts`, `get_post_analytics`: your drafts, queue, published posts and per-post results | Agent |
| `capture_substance`: save a story, opinion or number to your material bank | Agent |
| `write_post_in_my_voice`, `repurpose_post`, `generate_ideas`: ContentIn's own writer (Agent: 30 posts and 50 ideas a month; Agent Pro: 100 and 200) | Agent |
| `attach_images`: up to five images on a draft | Agent |
| `schedule_post`, `publish_post`: show the exact text, wait for your yes, then go through LinkedIn's official API | Agent, LinkedIn connected |
| `list_leads`, `list_my_comments`: people who engaged with your posts with ICP fit score; comments you left elsewhere | Agent Pro or Pro |

Agent plans allow at most 3 scheduled or published posts per profile per day.

## Safety

- Scheduling and publishing are two-step. The tool returns the exact text and a short-lived single-use token; nothing goes out until you confirm in your own words.
- One grant = one profile. The agent cannot reach other profiles, billing or LinkedIn credentials.
- The leads skill drafts only. It never sends comments, messages or connection requests.
- See `SECURITY.md` for reporting and for what is logged.

## Links

- Hub: https://contentin.io/linkedin-for-ai-agents/
- Setup guide: https://contentin.io/linkedin-mcp-server/setup/
- Privacy: https://www.iubenda.com/privacy-policy/58097432
- Terms: https://contentin.io/blog/linkedin-mcp-terms-of-service/
- Support: support@contentin.io

## Licence

MIT, ContentIn LLC. See `LICENSE`. The skills and configs in this repo are free to copy and adapt; the ContentIn service itself is a paid subscription governed by its own terms.
