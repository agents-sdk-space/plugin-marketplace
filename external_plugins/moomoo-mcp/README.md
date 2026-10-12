# moomoo plugin for Grok Build

Connect Grok Build to [moomoo](https://www.moomoo.com) quotes, stock screening, news, and account trading.

## Installation

In Grok Build, open `/plugin`, search for **moomoo**, and install.

That install is equivalent to:

```bash
grok mcp add moomoo-mcp --transport http https://mcp.moomoo.com/mcp
```

On first connection, Grok opens moomoo sign-in in the browser. Do not paste an API key into chat.

## Authentication

The plugin connects only to `https://mcp.moomoo.com/mcp`.

Network endpoints:

- `https://mcp.moomoo.com/mcp` — hosted MCP (Streamable HTTP)

Credentials: a moomoo account. Grok Build stores the token locally. No API key is stored in this plugin.

## Skills

| Skill | Purpose |
| --- | --- |
| `moomoo-mcp-quote` | Quotes, K-lines, order book, ticks, watchlists |
| `moomoo-mcp-screen` | Stock, warrant, option, and IPO screening |
| `moomoo-mcp-news` | News, financials, valuation, holders, capital flow |
| `moomoo-mcp-account` | Account, positions, and real or simulated orders |

Order placement, modification, and cancellation require a second confirmation in the skill instructions. The hosted MCP may also return `need_order_confirm` before an order takes effect.

## License

MIT. Adapted from the Futu MCP plugin skill guides for the moomoo hosted MCP.
