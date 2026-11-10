# Security

## Reporting a vulnerability

Email **support@contentin.io** with "security" in the subject. Include what you found, how to reproduce it and, if relevant, the client you used. We acknowledge within two working days and keep you informed until it is fixed.

Please do not open a public issue for a security problem and do not test against other people's ContentIn accounts.

## Scope

- This repository: skill instructions, plugin manifests and config snippets. The main risk here is a change that would make an agent skip the user's confirmation before scheduling or publishing, or leak the user's material. Report that like any other vulnerability.
- The ContentIn MCP server (`https://mcp.contentin.io/mcp-server`), the OAuth flow and API keys: also in scope, same address.

## What the connection can and cannot do

- One OAuth grant or API key is bound to one ContentIn profile. It cannot reach other profiles, billing or LinkedIn credentials.
- Scheduling and publishing are two-step: the tool returns the exact text and a short-lived single-use token; nothing goes out until the user confirms.
- Posting goes through LinkedIn's official API with the user's own LinkedIn authorisation.
- Revoke any grant or key at any time in ContentIn under Profiles, Connections.
- Tool calls are logged for abuse prevention (tool name, time, auth type, client, outcome, a one-way hash of the arguments). The content of requests and posts is not stored in that log.
