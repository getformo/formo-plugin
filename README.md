# Formo plugin

Connect AI agents to [Formo](https://formo.so), product analytics for onchain apps. Ask about visitors, connected wallets, transactions, revenue, funnels, retention, traffic sources, and wallet profiles in plain language. Build boards and charts, create segments, set alerts, and label wallets without leaving the chat.

This repo packages the Formo remote server and the `formo-analytics` skill for:

| Platform | Files |
|---|---|
| Claude (Claude.ai, Claude Code, Cowork) | `.claude-plugin/plugin.json`, `.mcp.json`, `skills/` |
| ChatGPT and Codex plugins | `plugin.json`, `mcp.json`, `skills/`, `assets/` |
| Gemini CLI | `gemini-extension.json` |
| MCP Registry | `server.json` |

## Connect

Server URL: `https://api.formo.so/v0/mcp/`

Sign in with OAuth and pick one project. You can also use a workspace API key as a bearer token. See the [setup guide](https://docs.formo.so/mcp/overview).

Claude Code:

```bash
claude plugin marketplace add getformo/formo-plugin
claude plugin install formo@formo-plugin
```

Gemini CLI:

```bash
gemini extensions install https://github.com/getformo/formo-plugin
```

## Data and safety

- Access is scoped to the project you choose at sign in.
- Read tools never change data. Tools that change or delete data are marked so your client asks before it runs them, and delete tools also need an explicit confirmation.
- Formo cannot move funds or sign transactions.

Privacy policy: https://formo.so/privacy. Terms: https://formo.so/tos. Support: https://formo.so/support.

## License

MIT
