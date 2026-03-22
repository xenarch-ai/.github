# /xenarch

**Payment infrastructure for the agentic internet.**

Xenarch routes micropayments between AI agents and content providers using the [x402 protocol](https://www.x402.org/) — HTTP 402 + USDC on Base. Non-custodial. 0% fee. Immutable smart contract.

## How it works

**For publishers** — monetize AI web scraping instead of blocking it:

```
AI agent ──► your site ──► 402 Payment Required + price
AI agent ──► pays USDC on Base
AI agent ──► your site ──► 200 + content
```

Set your payout wallet, configure pricing, serve `/.well-known/pay.json`. Done.

**For agents** — generate a wallet or connect your own, pay for gated content automatically:

```bash
npm install -g xenarch-cli
xenarch wallet generate       # create a new USDC wallet on Base
xenarch check <url>           # see if a URL is gated + pricing
xenarch pay <url>             # pay and get access
```

Private key stays on your machine (`~/.xenarch/config.json`). Fund the wallet with USDC on Base, and the CLI handles the rest — balance checks, on-chain payment, access token caching.

## Repos

| Package | What |
|---|---|
| [**pay-json**](https://github.com/xenarch-ai/pay-json) | pay.json open standard — machine-readable pricing for AI agents |
| [**xenarch-plugins**](https://github.com/xenarch-ai/xenarch-plugins) | WordPress plugin for AI bot detection and x402 payments |
| [**xenarch-js**](https://github.com/xenarch-ai/xenarch-js) | Client-side AI bot detection and payment gate (<9KB) |
| [**xenarch-contract**](https://github.com/xenarch-ai/xenarch-contract) | USDC splitter smart contract on Base L2 |
| [**xenarch-sdks**](https://github.com/xenarch-ai/xenarch-sdks) | SDKs, middleware, and CLI — npm, PyPI |
| [**xenarch-mcp**](https://github.com/xenarch-ai/xenarch-mcp) | MCP servers for AI agent payments and publisher setup |

## Links

- [xenarch.com](https://xenarch.com)
- [hello@xenarch.com](mailto:hello@xenarch.com)
