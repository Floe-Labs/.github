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
  <a href="https://basescan.org/address/0x17946cD3e180f82e632805e5549EC913330Bb175"><img src="https://img.shields.io/badge/Base-mainnet-blue" alt="Base mainnet" /></a>
</p>

---

## How it works

1. **Sign up with email + a funding source.** Card, Apple Pay, Google Pay, or bank transfer. Floe provisions your wallets in the background — no MetaMask, no seed phrase, no gas token.
2. **Floe issues an x402 credit line to your agent's wallet.** Set spending controls — per-call cap, daily limit, allowed destinations.
3. **Your agent pays vendors per-call; you get real-time visibility.** Every call is a typed receipt: target URL, amount, status, time. Reconcile, alert, or revoke from the dashboard.

---

## The Floe Stack

Everything your agent needs to earn, spend, and build credit. Six components. One SDK.

| # | Component | What it does | Status |
|---|---|---|---|
| 01 | **Agent Wallet** | Non-custodial smart-contract wallet with ERC-8004 identity, programmable spend limits, and allowed-destination permissions enforced on-chain. | `GA` |
| 02 | **Fiat on/off-ramp** | USDC in via cards, bank transfers, Apple Pay, Google Pay. Local payouts in 100+ countries on the way out. | Onramp `GA` · Offramp `Preview` |
| 03 | **Secured working capital** | Instant credit against on-chain collateral. One API call to borrow. **3,000+ lines issued · zero defaults.** | `GA` |
| 04 | **Unsecured working capital** | Credit underwritten against your agent's receivables and chain-of-thought signals. | `Preview` |
| 05 | **x402 payment facilitator** | One proxy endpoint to pay any of 13,000+ x402 APIs. Smart-contract enforced limits, ~50ms signing. | `GA` |
| 06 | **Credit & trust bureau** | Every repayment writes to a portable ERC-8004 record. Other protocols can underwrite your agent without re-running diligence. | Reader `Beta` · Writer `Preview` |

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
| **[agentkit-actions](https://github.com/Floe-Labs/agentkit-actions)** | The Floe SDK (TypeScript) — 45 actions covering wallet, secured credit, x402, agent awareness, and flash loans. | `npm install floe-agent` |
| **[agentkit-actions-py](https://github.com/Floe-Labs/agentkit-actions-py)** | The Floe SDK (Python) — same 45 actions, full parity. | `pip install floe-agentkit-actions` |
| **[floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server)** | The Floe stack exposed over MCP for Claude, Cursor, and any MCP-compatible agent. | [Setup guide](https://floe-labs.gitbook.io/docs/developers/mcp-server) |
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

// Borrow against on-chain collateral
const loan = await agent.run("instant_borrow", {
  borrowAmount: "5000000000",
  collateralAmount: "5500000000",
  maxInterestRateBps: "1200",
  duration: "604800",
});

// Pay any x402 API through the Floe facilitator
const response = await agent.run("x402_fetch", {
  url: "https://api.example.com/premium",
  method: "POST",
  body: { prompt: "..." },
});
```

### Python

```bash
pip install floe-agentkit-actions
```

```python
from floe_agentkit_actions import floe_action_provider

provider = floe_action_provider()

# Borrow against on-chain collateral
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

-> **[Full quickstart](https://floe-labs.gitbook.io/docs/getting-started/quickstart)**

---

## How it works — the full financial loop

1. **Setup** — register your agent and wallet. ERC-8004 identity, non-custodial wallet, programmable spend limits.
2. **Fund** — USDC in via cards, bank, Apple Pay, Google Pay, or on-chain.
3. **Borrow** — one API call to `instant_borrow`. Fixed rate, fixed term, isolated position.
4. **Spend** — `x402_fetch` against any x402 API. Floe signs, settles, verifies.
5. **Earn & repay** — agent collects revenue; `repay_loan` returns collateral atomically.
6. **Build trust** — every repayment writes to your agent's portable on-chain credit record.

---

## Protocol

| | |
|---|---|
| **Network** | Base mainnet |
| **Identity** | ERC-8004 agent record |
| **Primary market** | USDC/USDC, up to 99.5% LTV |
| **Volatile markets** | WETH, cbBTC collateral |
| **Loan tokens** | USDC, USDT |
| **Matcher proxy** | [`0x17946cD3e180f82e632805e5549EC913330Bb175`](https://basescan.org/address/0x17946cD3e180f82e632805e5549EC913330Bb175) |
| **x402 facilitator** | [`0x58EDdE022FFDAD3Fb0Fb0E7D51eb05AaF66a31f1`](https://basescan.org/address/0x58EDdE022FFDAD3Fb0Fb0E7D51eb05AaF66a31f1) |
| **Model** | Intent-based P2P matching, fixed rate, fixed term, per-loan isolated escrow |
| **Gas** | Free — Floe sponsors all transaction costs |
| **x402 APIs reachable** | 13,000+ via the Floe proxy |

---

## Links

- **Website:** [floelabs.xyz](https://floelabs.xyz)
- **Dashboard:** [dev-dashboard.floelabs.xyz](https://dev-dashboard.floelabs.xyz)
- **Docs:** [floe-labs.gitbook.io/docs](https://floe-labs.gitbook.io/docs)
- **X:** [@FloeLabs](https://x.com/FloeLabs)
- **Email:** hello@floelabs.xyz

---

<p align="center">
  <sub>The Financial OS for AI Agents.</sub>
</p>
