<!-- Banner: replace with your actual hosted image URL -->
<!-- <p align="center"><img src="https://floelabs.xyz/github-banner.png" alt="Floe Labs" width="100%" /></p> -->

<h1 align="center">Floe Labs</h1>

<p align="center">
  <strong>The onchain credit layer for AI agents.</strong>
</p>

<p align="center">
  Secured working capital on Base. Fixed rates. Per-loan isolated escrow. Gas-free for agents.
</p>

<p align="center">
  <a href="https://floelabs.xyz">Website</a> ·
  <a href="https://floe-labs.gitbook.io/docs">Docs</a> ·
  <a href="https://dev-dashboard.floelabs.xyz">App</a> ·
  <a href="https://x.com/FloeLabs">𝕏</a> 
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/floe-agent"><img src="https://img.shields.io/npm/v/floe-agent?label=npm&color=green" alt="npm" /></a>
  <a href="https://pypi.org/project/floe-agentkit-actions/"><img src="https://img.shields.io/pypi/v/floe-agentkit-actions?label=pypi&color=blue" alt="pypi" /></a>
  <a href="https://github.com/Floe-Labs/agentkit-actions/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-brightgreen" alt="license" /></a>
  <a href="https://basescan.org/address/0x17946cD3e180f82e632805e5549EC913330Bb175"><img src="https://img.shields.io/badge/Base-mainnet-blue" alt="Base mainnet" /></a>
</p>

---

## What we're building

Floe gives AI agents instant access to USDC working capital — without pre-funding wallets, without variable-rate pools, and with smart-contract-enforced repayment.

Agents post WETH or cbBTC as collateral → borrow USDC at a fixed rate → use it for API calls, compute, or any on-chain operation → repay when done, collateral returns automatically. **Gas-free — Floe sponsors all gas.**

---

## Repos

| Repo | What it does | Install |
|---|---|---|
| **[agentkit-actions](https://github.com/Floe-Labs/agentkit-actions)** | Coinbase AgentKit ActionProvider — 36 actions for lending, borrowing, flash loans, and x402 credit delegation (TypeScript) | `npm install floe-agent` |
| **[agentkit-actions-py](https://github.com/Floe-Labs/agentkit-actions-py)** | Same 36 actions for Python (full parity) | `pip install floe-agentkit-actions` |
| **[floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server)** | MCP server for Claude Desktop, Cursor, and any MCP-compatible agent | [Setup guide](https://floe-labs.gitbook.io/docs/developers/mcp-server) |

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

// Borrow 1,000 USDC against 0.5 WETH
const loan = await agent.run("instant_borrow", {
  marketId: "USDC/WETH",
  borrowAmount: "1000000000",
  collateralAmount: "500000000000000000",
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
# Register with your AgentKit agent
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

→ **[Full quickstart](https://floe-labs.gitbook.io/docs/agents/quickstart-agents)**

---

## Protocol

| | |
|---|---|
| **Network** | Base mainnet |
| **Loan tokens** | USDC, USDT |
| **Collateral** | WETH, cbBTC |
| **Matcher proxy** | [`0x17946cD3e180f82e632805e5549EC913330Bb175`](https://basescan.org/address/0x17946cD3e180f82e632805e5549EC913330Bb175) |
| **Model** | Intent-based P2P matching, fixed rate, fixed term, per-loan isolated escrow |

---

## Links

- **Website:** [floelabs.xyz](https://floelabs.xyz)
- **App:** [app.floelabs.xyz](https://dev-dashboard.floelabs.xyz)
- **Docs:** [floe-labs.gitbook.io/docs](https://floe-labs.gitbook.io/docs)
- **𝕏:** [@FloeLabs](https://x.com/FloeLabs)
- **Email:** hello@floelabs.xyz

---

<p align="center">
  <sub>Building the credit layer for the agent economy.</sub>
</p>
