<p align="center"><img src="https://raw.githubusercontent.com/Floe-Labs/.github/main/profile/banner.png" alt="Floe Labs" width="100%" /></p>

<h1 align="center">Floe Labs</h1>

<p align="center">
  <strong>Credit and payments for AI agent developers.</strong><br/>
  x402 credit lines, fiat funding, programmable spend controls. No crypto required.
</p>

<p align="center">
  <a href="https://floelabs.xyz">Website</a> ·
  <a href="https://floe-labs.gitbook.io/docs">Docs</a> ·
  <a href="https://dev-dashboard.floelabs.xyz">Dashboard</a> ·
  <a href="https://x.com/FloeLabs">&#x1D54F;</a>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/floe-agent"><img src="https://img.shields.io/npm/v/floe-agent?label=npm&color=green" alt="npm" /></a>
  <a href="https://pypi.org/project/floe-agentkit-actions/"><img src="https://img.shields.io/pypi/v/floe-agentkit-actions?label=pypi&color=blue" alt="pypi" /></a>
  <a href="https://github.com/Floe-Labs/agentkit-actions/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-brightgreen" alt="license" /></a>
</p>

> **$2 free credit (~200 API calls).** Your agent can start paying for APIs today — no card required. [Get started →](https://dev-dashboard.floelabs.xyz)

---

## How it works

1. **Sign up with email + a funding source.** Card, Apple Pay, Google Pay, or bank transfer. Floe provisions your wallets in the background — no MetaMask, no seed phrase, no gas token.
2. **Floe issues an x402 credit line to your agent's wallet.** Set spending controls — per-call cap, daily limit, allowed destinations.
3. **Your agent pays vendors per-call; you get real-time visibility.** Every call is a typed receipt: target URL, amount, status, time. Reconcile, alert, or revoke from the dashboard.

---

## Vendor Marketplace — 27 verified API endpoints

Every endpoint is callable with one Floe API key. [Browse the full directory →](https://floe-labs.gitbook.io/docs/x402-directory)

| Category | Services |
|----------|----------|
| **Compute** | Venice AI — chat, responses API, embeddings |
| **Voice** | Venice AI — TTS, transcription · dTelecom STT |
| **Image** | Venice AI — generation, upscale, edit, background removal |
| **Text** | Firecrawl — search + scrape |
| **Search** | Exa, Parallel AI, Tavily |
| **Browser** | Hyperbrowser, Browserbase, Anchor Browser |
| **Agent Tools** | AgentMail, Pinata Cloud, PostalForm |

---

## The Floe Stack

| # | Component | What it does | Status |
|---|---|---|---|
| 01 | **Agent Wallet** | Non-custodial wallet with programmable spend limits and allowed-destination controls. | `GA` |
| 02 | **Fiat on/off-ramp** | USDC in via cards, bank transfers, Apple Pay, Google Pay. Local payouts in 100+ countries. | Onramp `GA` · Offramp `Preview` |
| 03 | **Secured working capital** | Instant credit against your deposit. One API call to borrow. **3,000+ lines issued · zero defaults.** | `GA` |
| 04 | **Unsecured working capital** | Credit underwritten against your agent's receivables and usage signals. | `Preview` |
| 05 | **x402 payment facilitator** | One proxy endpoint to pay any x402 API. 27 verified endpoints in the [Vendor Marketplace](https://floe-labs.gitbook.io/docs/x402-directory). | `GA` |
| 06 | **Credit & trust bureau** | Every repayment builds your agent's portable credit record. | Reader `Beta` · Writer `Preview` |

---

## Works with your framework

| Framework | Status | How |
|---|---|---|
| Coinbase AgentKit | `GA` | Native — `floeActionProvider` |
| LangChain | `GA` | Via `getLangChainTools` adapter |
| Vercel AI SDK | `GA` | Via `getVercelAITools` adapter |
| Claude Desktop / Claude Code / Cursor | `GA` | Via [floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server) |
| CrewAI | `Beta` | Via MCP server |
| OpenAI Agents SDK | `Preview` | MCP fallback today; native adapter on the way |
| ElizaOS | `Preview` | MCP fallback today |
| Plain HTTP / REST | `GA` | Any framework that speaks HTTP |

---

## Repos

| Repo | What it does | Install |
|---|---|---|
| **[agentkit-actions](https://github.com/Floe-Labs/agentkit-actions)** | TypeScript SDK — 45 actions covering wallet, credit, x402, agent awareness, and flash loans. | `npm install floe-agent` |
| **[agentkit-actions-py](https://github.com/Floe-Labs/agentkit-actions-py)** | Python SDK — same 45 actions, full parity. | `pip install floe-agentkit-actions` |
| **[floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server)** | MCP server for Claude, Cursor, and any MCP-compatible agent. | [Setup guide](https://floe-labs.gitbook.io/docs/developers/mcp-server) |
| **[floe-examples](https://github.com/Floe-Labs/floe-examples)** | Runnable end-to-end agents across frameworks. | `git clone` |

---

## Get started in 5 minutes

### TypeScript

```bash
npm install floe-agent @coinbase/agentkit viem zod
```

```typescript
import { AgentKit } from "@coinbase/agentkit";
import { floeActionProvider } from "floe-agent";

const agent = await AgentKit.from({
  walletProvider,
  actionProviders: [floeActionProvider()],
});

// Borrow against your deposit
const loan = await agent.run("instant_borrow", {
  borrowAmount: "5000000000",
  collateralAmount: "5500000000",
  maxInterestRateBps: "1200",
  duration: "604800",
});

// Pay any x402 API through the Floe proxy
const response = await agent.run("x402_fetch", {
  url: "https://api.exa.ai/search",
  method: "POST",
  body: { query: "AI agent frameworks" },
});
```

### Python

```bash
pip install floe-agentkit-actions
```

```python
from floe_agentkit_actions import floe_action_provider

provider = floe_action_provider()

loan = provider.instant_borrow(wallet_provider, {
    "borrow_amount": "5000000000",
    "collateral_amount": "5500000000",
    "max_interest_rate_bps": "1200",
    "duration": "604800",
})
```

### MCP (zero install)

Add to your Claude Desktop, Claude Code, or Cursor config:

```json
{
  "mcpServers": {
    "floe": {
      "url": "https://mcp.floelabs.xyz/mcp",
      "transport": "streamable-http"
    }
  }
}
```

→ **[Full quickstart](https://floe-labs.gitbook.io/docs/getting-started/quickstart)**

---

## Links

- **Website:** [floelabs.xyz](https://floelabs.xyz)
- **Dashboard:** [dev-dashboard.floelabs.xyz](https://dev-dashboard.floelabs.xyz)
- **Docs:** [floe-labs.gitbook.io/docs](https://floe-labs.gitbook.io/docs)
- **X:** [@FloeLabs](https://x.com/FloeLabs)
- **Email:** hello@floelabs.xyz

---

<p align="center">
  <sub>Credit and payments for the agent economy.</sub>
</p>
