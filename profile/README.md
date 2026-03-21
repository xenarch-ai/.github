# /xenarch

**Payment infrastructure for the agentic internet.**

Xenarch routes micropayments between AI agents and content providers using the [x402 protocol](https://www.x402.org/) — HTTP 402 + USDC on Base. Non-custodial. 0% fee. Immutable smart contract.

## How it works

When an AI agent requests content from a Xenarch-protected site, the server returns **HTTP 402 (Payment Required)** with pricing info. The agent pays a USDC micropayment on Base L2, and the server grants access. Settlement in under 2 seconds.

```
Agent ──► Site ──► 402 + price
Agent ──► pays USDC on Base
Agent ──► Site ──► 200 + content
```

## Repos

| Package | What |
|---|---|
| [**pay-json**](https://github.com/xenarch-ai/pay-json) | pay.json open standard — machine-readable pricing for AI agents |
| [**xenarch-plugins**](https://github.com/xenarch-ai/xenarch-plugins) | WordPress plugin for AI bot detection and x402 payments |
| [**xenarch-js**](https://github.com/xenarch-ai/xenarch-js) | Client-side AI bot detection and payment gate (<9KB) |
| [**xenarch-contract**](https://github.com/xenarch-ai/xenarch-contract) | USDC splitter smart contract on Base L2 |
| [**xenarch-sdks**](https://github.com/xenarch-ai/xenarch-sdks) | SDKs and middleware — npm, PyPI, CLI |
| [**xenarch-mcp**](https://github.com/xenarch-ai/xenarch-mcp) | MCP servers for AI agent payments |

## Links

- [xenarch.com](https://xenarch.com)
- [hello@xenarch.com](mailto:hello@xenarch.com)
