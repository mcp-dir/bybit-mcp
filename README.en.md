# Bybit

### Bybit for Claude, ChatGPT and AI agents

Bybit crypto exchange, unified account and Funding wallet balances, open derivatives positions, orders, executions with per-trade fees, loans, bots and market quotes, via the official V5 REST API, with full read and write coverage. Placing and cancelling orders needs a key with trade permission. Withdrawals and wallet transfers are not exposed. Auth with an api_key and api_secret generated in your Bybit account.

- 📊 **1 tool**
- 🔒 **Read-only**
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Magic-link login (no password)**

[Portuguese version](README.md) · [Full docs (PT-BR)](docs/)

---

## One-click install

### Claude (Web and Desktop)

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → name `Bybit`, URL `https://api.mcp.ai/p_bybit`.

### Cursor

[➕ Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=bybit&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9ieWJpdCJ9)

### VS Code (Copilot Chat)

[➕ Install in VS Code](vscode:mcp/install?name=bybit&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_bybit%22%7D)

### Any other MCP-over-HTTP client

```
https://api.mcp.ai/p_bybit
```

---

## 1 tool

| Tool | Description |
|---|---|
| `search_tools` | Single entrypoint for MCP catalog. |

---

## Pricing

See [docs/precos.md](docs/precos.md) (PT-BR).

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_bybit` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
