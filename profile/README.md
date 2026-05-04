# /xenarch

**Payment infrastructure for the agentic internet.**

Xenarch is a non-custodial, facilitator-agnostic implementation of the [x402 protocol](https://www.x402.org/) for AI agents and publishers. AI agents — Claude, Cursor, LangChain, CrewAI, AutoGen, LangGraph — pay HTTP 402-gated APIs and content with gasless USDC micropayments on Base L2. Publishers monetize bots and crawlers per request without subscriptions, API keys, or card processors. Settlement is direct from agent wallet to publisher wallet via competing x402 facilitators (PayAI, xpay, Ultravioleta DAO, x402.rs). There is no Xenarch contract in the money flow. 0% fee, structurally.

## Why

- **Non-custodial.** Agent pays publisher wallet directly. Xenarch never holds, touches, or signs for funds.
- **Facilitator-agnostic.** Each gate publishes a ranked list of x402 facilitators. The SDK picks one. No vendor lock-in.
- **Gasless.** Facilitators sponsor gas. Agents carry USDC, nothing else.
- **0% fee, as architecture.** No Xenarch contract on the payment path means nothing to skim. Not a policy that could change.
- **Open standards.** [x402](https://www.x402.org/) (payment protocol) + [pay.json](https://github.com/xenarch-ai/pay-json) (machine-readable pricing — robots.txt for payments, authored by Xenarch).

## Install

**Agent — MCP server (Claude Desktop, Cursor, Cline, any MCP client):**

```bash
claude mcp add xenarch -- npx @xenarch/agent-mcp
```

**Agent — Python SDK (LangChain, CrewAI, AutoGen, LangGraph, raw):**

```bash
pip install xenarch[langchain,x402]
```

**Publisher — drop-in middleware:**

| Stack | Install |
|---|---|
| FastAPI | `pip install xenarch[fastapi]` |
| WordPress | [xenarch-plugins/wordpress](https://github.com/xenarch-ai/xenarch-plugins) |
| Joomla | [xenarch-plugins/joomla](https://github.com/xenarch-ai/xenarch-plugins) |
| Cloudflare Worker | [xenarch-plugins/cloudflare](https://github.com/xenarch-ai/xenarch-plugins) |

**Manage — CLI for sites, pricing, history, wallet:**

```bash
npx xenarch
```

## How it works

```
1. Agent calls a URL.
   Server returns HTTP 402 + price + ranked facilitator list.

2. SDK signs an EIP-3009 USDC transferWithAuthorization,
   submits via the chosen facilitator (gasless),
   re-fetches the resource with proof of payment.

3. Server verifies on-chain; agent gets the content.
```

No API keys. No signup. No custodial balance. Every payment is an on-chain USDC transfer that agent and publisher can verify on Basescan.

## Repos

| Package | What |
|---|---|
| [**xenarch-mcp**](https://github.com/xenarch-ai/xenarch-mcp) | x402 MCP server — `@xenarch/agent-mcp` on npm. Headline install surface for AI agents. |
| [**xenarch-sdks**](https://github.com/xenarch-ai/xenarch-sdks) | Python SDK + TypeScript CLI. `pip install xenarch`, `npx xenarch`. |
| [**x402-agent**](https://github.com/xenarch-ai/x402-agent) | Framework-agnostic x402 payer. Works in LangChain, CrewAI, AutoGen, LangGraph, or any agent framework. |
| [**xenarch-plugins**](https://github.com/xenarch-ai/xenarch-plugins) | Publisher plugins — WordPress, Joomla, Cloudflare Worker. |
| [**xenarch-js**](https://github.com/xenarch-ai/xenarch-js) | Client-side AI bot detection + payment-gate snippet (<9KB). |
| [**pay-json**](https://github.com/xenarch-ai/pay-json) | pay.json open standard — machine-readable pricing for AI agents. |
| [**xenarch-examples**](https://github.com/xenarch-ai/xenarch-examples) | Working integrations — Python, LangChain, CrewAI, AutoGen, LangGraph, Claude Desktop, publisher middleware. |
| [**xenarch-docs**](https://github.com/xenarch-ai/xenarch-docs) | Developer docs — [docs.xenarch.com](https://docs.xenarch.com) (Mintlify). |
| [**xenarch-web**](https://github.com/xenarch-ai/xenarch-web) | [xenarch.com](https://xenarch.com) website + publisher dashboard. |
| [xenarch-contract](https://github.com/xenarch-ai/xenarch-contract) | **Archived.** Original USDC splitter contract; immutable on-chain at `0xC6D3a6B6fcCD6319432CDB72819cf317E88662ae` but no longer in the money flow post-pivot. |

## Landscape

|  | Cloudflare PPC | TollBit | Stripe MPP | **Xenarch** |
|---|---|---|---|---|
| Works on any host | ✗ (Cloudflare-only) | ✗ (enterprise only) | ✓ (Stripe account req.) | ✓ (any host) |
| Non-custodial | ✗ | ✗ | ✗ (Stripe holds balance) | ✓ (direct on-chain) |
| Gasless for agent | n/a | n/a | ✗ | ✓ (facilitator-sponsored) |
| 0% fee | ✗ | ✗ | ✗ (Stripe pricing) | ✓ (no contract on path) |
| Open standard | ✗ | ✗ | ✗ (proprietary MPP) | ✓ (x402 + pay.json) |
| API keys / signup | ✗ | ✗ | ✗ | ✓ (none, auto-wallet) |
| Settlement chain | off-chain | off-chain | Tempo L1 (Stripe-co-owned) | Base L2 (open) |

## Links

- Website — [xenarch.com](https://xenarch.com)
- Docs — [docs.xenarch.com](https://docs.xenarch.com)
- npm — [@xenarch/agent-mcp](https://www.npmjs.com/package/@xenarch/agent-mcp), [xenarch (CLI)](https://www.npmjs.com/package/xenarch)
- PyPI — [xenarch](https://pypi.org/project/xenarch/)
- Smithery — [xenarch/xenarch-mcp](https://smithery.ai/servers/xenarch/xenarch-mcp)
- Glama — [xenarch-ai/xenarch-mcp](https://glama.ai/mcp/servers/xenarch-ai/xenarch-mcp)
- Email — [hello@xenarch.com](mailto:hello@xenarch.com)
