<div align="center">

# Gatefare

**Non-custodial x402 marketplace for paid HTTP APIs.**
USDC settlement on Base. No custody, no signups for buyers, no gatekeepers.

[gatefare.io](https://gatefare.io) · [docs](https://gatefare.io/docs) · [@Gatefareio](https://twitter.com/Gatefareio)

</div>

---

### What we ship

| | |
|---|---|
| 🔌 **MCP server** for Claude/Cursor/agents — [`@gatefare/mcp`](https://www.npmjs.com/package/@gatefare/mcp) ([repo](https://github.com/gatefareio/mcp-server)) | Discover, buy, and publish APIs from any AI agent |
| 🌐 **Marketplace** at [gatefare.io](https://gatefare.io) | List your API → get a paid proxy URL → earn USDC per call |
| 📜 **Open standards** — [x402](https://x402.org) for payments, [MCP](https://modelcontextprotocol.io) for agent integration | No vendor lock-in, no custody, no API keys to revoke |

### How it works

1. **Publishers** register an API → Gatefare returns a proxy URL with a price tag
2. **Buyers** call the proxy → it returns 402 → buyer signs an EIP-3009 USDC transfer → call retried with payment → upstream response returned
3. **Payment** settles on Base mainnet directly to a Splits contract — Gatefare never holds funds

### Links

- 🌍 Site & catalog: [gatefare.io](https://gatefare.io)
- 📖 API docs: [gatefare.io/docs](https://gatefare.io/docs)
- 🤖 LLM context: [gatefare.io/llms-full.txt](https://gatefare.io/llms-full.txt)
- 🔧 OpenAPI spec: [gatefare.io/openapi.json](https://gatefare.io/openapi.json)
- 🐦 Twitter: [@Gatefareio](https://twitter.com/Gatefareio)
- 📧 Contact: [official@gatefare.io](mailto:official@gatefare.io)

### Standards we follow

[![x402](https://img.shields.io/badge/payments-x402-purple)](https://x402.org)
[![MCP](https://img.shields.io/badge/agents-MCP-blue)](https://modelcontextprotocol.io)
[![Base](https://img.shields.io/badge/network-Base-0052ff)](https://base.org)
[![USDC](https://img.shields.io/badge/asset-USDC-2775ca)](https://www.circle.com/usdc)
