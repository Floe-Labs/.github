<p align="center"><img src="https://raw.githubusercontent.com/Floe-Labs/.github/main/profile/banner.png" alt="Floe Labs" width="100%" /></p>

<h1 align="center">Floe Labs</h1>

<p align="center">
  <strong>Working capital for AI agents.</strong>
</p>

<p align="center">
  Deposit USDC, borrow up to 95% — fixed rates, gas-free, no crypto complexity.<br/>
  3,000+ secured working capital lines issued. Zero defaults.
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

## What we're building

Floe gives AI agents instant access to USDC working capital on Base.

**The simple story:** deposit USDC as collateral, borrow up to 95% as a credit line. Same-token market — no price-volatility risk, no liquidation surprises. Fixed rates, per-loan isolated escrow. **Gas-free — Floe sponsors all transaction costs.**

**Fund with fiat:** Agents (or their operators) can fund wallets with USDC via Coinbase — credit card or bank transfer — directly from the [Floe dashboard](https://dev-dashboard.floelabs.xyz). No crypto on-ramp needed.

Also supports WETH and cbBTC collateral for volatile markets and crypto-native agents.

---

## Repos

| Repo | What it does | Install |
|---|---|---|
| **[agentkit-actions](https://github.com/Floe-Labs/agentkit-actions)** | Coinbase AgentKit ActionProvider — 45 actions for USDC credit lines, lending, flash loans, and x402 credit delegation (TypeScript) | `npm install floe-agent` |
| **[agentkit-actions-py](https://github.com/Floe-Labs/agentkit-actions-py)** | Same 45 actions for Python (full parity) | `pip install floe-agentkit-actions` |
| **[floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server)** | MCP server for Claude Desktop, Cursor, and any MCP-compatible agent | [Setup guide](https://floe-labs.gitbook.io/docs/developers/mcp-server) |
| **[floe-examples](https://github.com/Floe-Labs/floe-examples)** | Runnable example agents and integration recipes | `git clone` |

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

// Deposit 10,000 USDC, borrow 9,500 USDC — same-token market, no price risk
const loan = await agent.run("instant_borrow", {
  borrowAmount: "9500000000",
  collateralAmount: "10000000000",
  maxInterestRateBps: "800",
  duration: "1209600",
});
```

### Python

```bash
pip install floe-agentkit-actions
```

```python
from floe_agentkit_actions import floe_action_provider

provider = floe_action_provider()

# Deposit 10,000 USDC, borrow 9,500 USDC
result = provider.instant_borrow(wallet_provider, {
    "borrow_amount": "9500000000",
    "collateral_amount": "10000000000",
    "max_interest_rate_bps": "800",
    "duration": "1209600",
})
```

### MCP (zero install)

Add to your Claude Desktop or Cursor config:

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

-> **[Full quickstart](https://floe-labs.gitbook.io/docs/agents/quickstart-agents)**

---

## Protocol

| | |
|---|---|
| **Network** | Base mainnet |
| **Primary market** | USDC/USDC (deposit USDC, borrow up to 95%) |
| **Volatile markets** | WETH, cbBTC collateral |
| **Loan tokens** | USDC, USDT |
| **Matcher proxy** | [`0x17946cD3e180f82e632805e5549EC913330Bb175`](https://basescan.org/address/0x17946cD3e180f82e632805e5549EC913330Bb175) |
| **Facilitator** | [`0x58EDdE022FFDAD3Fb0Fb0E7D51eb05AaF66a31f1`](https://basescan.org/address/0x58EDdE022FFDAD3Fb0Fb0E7D51eb05AaF66a31f1) |
| **Model** | Intent-based P2P matching, fixed rate, fixed term, per-loan isolated escrow |
| **Gas** | Free — Floe sponsors all transaction costs |
| **Fund with fiat** | Credit card or bank transfer via Coinbase from the dashboard |

---

## Links

- **Website:** [floelabs.xyz](https://floelabs.xyz)
- **Dashboard:** [dev-dashboard.floelabs.xyz](https://dev-dashboard.floelabs.xyz)
- **Docs:** [floe-labs.gitbook.io/docs](https://floe-labs.gitbook.io/docs)
- **X:** [@FloeLabs](https://x.com/FloeLabs)
- **Email:** hello@floelabs.xyz

---

<p align="center">
  <sub>Working capital for the agent economy.</sub>
</p>
