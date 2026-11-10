# Contributing

Thanks for helping make these skills better.

## What this repo is

Two agent skills (`skills/*/SKILL.md`), a Claude Code plugin manifest (`.claude-plugin/`) and ready-made MCP client configs (`mcp/`). No code. The MCP server itself is closed source and runs at `https://mcp.contentin.io/mcp-server`; issues with the server or its tools go to support@contentin.io, not to this repo.

## Changes we take

- Clearer instructions in a `SKILL.md`, fixes to tool names, plan requirements or refusal codes.
- New or corrected client config snippets in `mcp/` (say which client and version you tested on).
- Typos, wording, README fixes.

## Rules

- Keep `SKILL.md` within the Agent Skills spec (https://agentskills.io/specification): `name` matches the folder, lowercase and hyphens; `description` under 1024 characters; body under 500 lines.
- Never add a credential, token or key, not even a fake-looking one. Use `<your key>` in examples.
- Do not add anything that sends, posts or scrapes on LinkedIn without the user's explicit, in-conversation confirmation. The confirmation rule in `skills/contentin-linkedin/SKILL.md` is not negotiable.
- One change per pull request, with a one-paragraph description of what you tested and in which agent.

## Process

1. Fork, branch, edit.
2. If Claude Code is installed, run `claude plugin validate --strict .` from the repo root.
3. Open a pull request. We review within a few working days.

By contributing you agree your contribution is licensed under the MIT licence in `LICENSE`.
