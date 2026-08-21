# Bybit

### Bybit para Claude, ChatGPT e agentes de IA

Exchange de criptomoedas Bybit, saldo da conta unificada e da carteira Funding, posições abertas em derivativos, ordens, execuções com taxa por trade, empréstimos, bots e cotação de mercado, via API REST oficial V5, com cobertura total de leitura e de escrita. Criar e cancelar ordem exigem uma chave com permissão de negociação. Saque e transferência entre carteiras não são expostos. Autenticação por api_key e api_secret gerados na sua conta Bybit.

- 📊 **1 ferramenta**
- 🔒 **Somente leitura**
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Login via magic-link (sem senha)**

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `Bybit` e **URL** `https://api.mcp.ai/p_bybit`.

### Cursor

[➕ Instalar Bybit no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=bybit&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9ieWJpdCJ9)

### VS Code (Copilot Chat)

[➕ Instalar Bybit no VS Code](vscode:mcp/install?name=bybit&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_bybit%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_bybit
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Qual meu saldo total na Bybit?
Quais posições eu tenho abertas e qual o resultado não realizado?
Quanto paguei de taxa nos meus trades da última semana?
```

---

## 1 ferramenta disponível

| Tool | Descrição |
|---|---|
| `search_tools` | Single entrypoint for MCP catalog. |

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Planos a partir do tier grátis. Veja [docs/precos.md](docs/precos.md).

---

## Privacidade & LGPD

- **Somente leitura**, nenhuma ferramenta altera dados na origem.
- **Sub-processadores**: Bybit, o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills — tudo MIT.

**Posso usar com agente próprio (não Claude/Cursor)?**
Sim — qualquer cliente que suporte MCP over HTTP. URL: `https://api.mcp.ai/p_bybit`.


---

## Suporte

- 📧 [bybit@mcp.ai](mailto:bybit@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/bybit-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_bybit` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
