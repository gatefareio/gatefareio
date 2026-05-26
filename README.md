<div align="center">

# Gatefare

**Non-custodial x402 marketplace for paid HTTP APIs.**
USDC settlement on Base. No custody, no signups for buyers, no gatekeepers.

[gatefare.io](https://gatefare.io) · [docs](https://gatefare.io/docs) · [@Gatefareio](https://twitter.com/Gatefareio)

</div>

---

### What we ship

| Package | Use case | Install |
|---|---|---|
| 🤖 [`@gatefare/mcp`](https://www.npmjs.com/package/@gatefare/mcp) | MCP server. Drop into Claude Desktop, Cursor, Cline, or any MCP host so an agent can discover, buy, and publish paid APIs. | `npx @gatefare/mcp` |
| 📦 [`@gatefare/client`](https://www.npmjs.com/package/@gatefare/client) | TypeScript SDK. Build Node/TS agents that pay HTTP 402 APIs in USDC. Built-in spend caps + claim retry. LangChain / LlamaIndex / OpenAI / Anthropic tool adapters bundled. | `npm install @gatefare/client` |
| 🐍 [`gatefare`](https://pypi.org/project/gatefare/) | Python SDK. Same primitives in Python. LangChain Python, LlamaIndex, OpenAI, Anthropic adapters. | `pip install gatefare` |
| 🌐 [gatefare.io](https://gatefare.io) | Marketplace. List your API, get a paid proxy URL, earn USDC per call. | |

### How it works

1. **Publishers** register an API. Gatefare returns a proxy URL with a price tag and an immutable on-chain 0xSplits contract that routes 90 percent to the publisher and 10 percent to the platform.
2. **Buyers** call the proxy. It returns HTTP 402. The buyer (an agent through one of our SDKs, or a human through a browser pay page) signs an EIP-3009 USDC transfer. The call is retried with an `X-Payment` header and the upstream response is returned.
3. **Settlement** lands on Base mainnet directly into the Splits contract. Gatefare never holds funds. If upstream fails after settle, the buyer has a 24h / 10-attempt free retry budget via `/p/_claim/<id>`.

### Quick start for buyers

**TypeScript agent paying a Gatefare API:**

```ts
import { Gatefare } from "@gatefare/client";

const gf = new Gatefare({
  wallet: { privateKey: process.env.WALLET_PRIVATE_KEY! },
  spendCaps: { perCallUsdc: 0.10, perDayUsdc: 5.00 },
});

const apis = await gf.listCatalog({ priceLimitUsdc: 0.05, limit: 5 });
const result = await gf.callApi(apis[0].slug, { query: { city: "Berlin" } });
console.log(result.status, result.data);
```

**Same flow in Python:**

```python
from gatefare import Gatefare

gf = Gatefare(
    wallet_private_key=os.environ["WALLET_PRIVATE_KEY"],
    spend_caps={"per_call_usdc": 0.10, "per_day_usdc": 5.00},
)

apis = gf.list_catalog(price_limit_usdc=0.05, limit=5)
result = gf.call_api(apis[0].slug, query={"city": "Berlin"})
print(result.status, result.data)
```

**Inside any MCP host (Claude Desktop, Cursor, Cline):**

```json
{
  "mcpServers": {
    "gatefare": {
      "command": "npx",
      "args": ["-y", "@gatefare/mcp"],
      "env": {
        "GATEFARE_WALLET_PRIVATE_KEY": "0x...",
        "GATEFARE_AUTO_PAY_CAP_USDC": "1.00"
      }
    }
  }
}
```

The agent gets 15 tools for catalog discovery, paid calls, publisher operations, and trust checks (publisher reputation, sample-response inspection).

### Quick start for publishers

1. Sign up at [gatefare.io](https://gatefare.io).
2. Add your API endpoint URL, a sample response, and a price per call.
3. Receive a proxy URL like `https://gatefare.io/p/<handle>/<api-name>`.
4. Share it. Buyers call it. USDC accumulates in your Splits contract on Base.
5. Run `distribute()` to pull funds to your wallet. The Gatefare operator pays the gas.

You never share a private key with Gatefare. You never custody anyone else's funds. The Splits contract is immutable after deploy. Nobody (including us) can redirect your share.

### Trust signals built in

Every paid call is protected by:

- **On-chain settle reconciliation.** We cross-check the facilitator's `200 OK` against `eth_getTransactionReceipt` to detect reverted settles before the upstream fires.
- **Sanctions screening.** OFAC plus EU plus UN plus mixers plus Chainalysis, evaluated before settle.
- **Circuit breaker per API.** A broken upstream stops accepting payments before USDC leaves the wallet.
- **24h / 10-attempt free retry** via `/p/_claim/<id>` if upstream fails after a successful settle.
- **Publisher reputation badges** (Established, Top contributor, Highly rated) visible to buyers before they pay.

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
