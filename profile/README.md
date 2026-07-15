<p align="center"><img src="https://raw.githubusercontent.com/Floe-Labs/.github/main/profile/banner.png" alt="Floe Labs" width="100%" /></p>

# Floe Labs

**The spend layer for AI agents.** One endpoint to pay across any LLM or voice vendor API services,
with programmable, context-aware budgets. Walletless.

[Website](https://floelabs.xyz) · [Docs](https://floe-labs.gitbook.io/docs) · [Dashboard](https://dev-dashboard.floelabs.xyz) · [𝕏 @FloeLabs](https://x.com/FloeLabs)

[![npm](https://img.shields.io/npm/v/floe-agent?label=npm&color=green)](https://www.npmjs.com/package/floe-agent)
[![pypi](https://img.shields.io/pypi/v/floe-agentkit-actions?label=pypi&color=blue)](https://pypi.org/project/floe-agentkit-actions/)
[![license](https://img.shields.io/badge/license-MIT-brightgreen)](https://github.com/Floe-Labs/agentkit-actions/blob/main/LICENSE)

---

> **Start free.** 200 API credits on signup — no card, no wallet.
> Your agent makes its first paid API call in minutes. [Get started →](https://dev-dashboard.floelabs.xyz)

## Why Floe

Your agent calls a dozen paid APIs — LLMs, voice, search, data. That's a dozen
accounts, a dozen prepaid balances, a dozen keys, and no unified way to see or
govern what your agent spends. Agents overspend, loop, and stall.

Floe gives your agent **a budget, not a balance**:

- **One endpoint, 2,000+ LLM inference + vendor API services.** Pay any vendor through Floe. No per-vendor accounts or keys.
- **Programmable spend controls.** Per-call caps, daily limits, allowed destinations — set at the vendor, agent, or team level, time-bound. Enforced *before* money moves.
- **Context-aware budgets.** Your agent senses when it's near its limit mid-task and adapts (e.g. downgrades to a cheaper model) instead of hard-stopping.
- **Walletless.** Email + a funding source. We provision wallets in the background — no MetaMask, no seed phrase, no gas. The stablecoin rails are invisible.
- **Real-time visibility.** Every call is a typed receipt: target, amount, status, time. Reconcile, alert, or revoke from the dashboard.

## Quickstart (5 minutes)

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

// Pay any x402 API through the Floe proxy — your agent never touches the payment layer
const res = await agent.run("x402_fetch", {
  url: "https://api.exa.ai/search",
  method: "POST",
  body: { query: "AI agent frameworks" },
});
```

```bash
pip install floe-agentkit-actions
```

```python
from floe_agentkit_actions import floe_action_provider

provider = floe_action_provider()
res = provider.x402_fetch(wallet_provider, {
    "url": "https://api.exa.ai/search",
    "method": "POST",
    "body": {"query": "AI agent frameworks"},
})
```

**MCP (zero install)** — add to Claude Desktop / Claude Code / Cursor:

```json
{ "mcpServers": { "floe": {
  "url": "https://mcp.floelabs.xyz/mcp",
  "transport": "streamable-http"
} } }
```

→ [Full quickstart](https://floe-labs.gitbook.io/docs/developers/agent-quickstart)

## Vendor Marketplace — 2,000+ vendor API services, one key

| Category | Services |
|---|---|
| Compute | Venice AI (chat, responses, embeddings) | OpenAI | z.ai | Kimi | Anthropic | Google Gemini
| Voice | Venice AI (TTS, transcription) · dTelecom STT |
| Image | Venice AI (generation, upscale, edit, background removal) |
| Web | Firecrawl (search + scrape) |
| Search | Exa · Parallel AI · Tavily |
| Browser | Hyperbrowser · Browserbase · Anchor Browser |
| Agent tools | AgentMail · Pinata · PostalForm |

[Browse the full directory →](https://floe-labs.gitbook.io/docs/x402-directory)

## Works with your framework

| Framework | Status | How |
|---|---|---|
| Coinbase AgentKit | GA | Native — `floeActionProvider` |
| LangChain | GA | `getLangChainTools` adapter |
| Vercel AI SDK | GA | `getVercelAITools` adapter |
| Claude / Cursor | GA | `floe-mcp-server` |
| CrewAI | Beta | via MCP server |
| OpenAI Agents SDK | Preview | MCP fallback; native adapter in progress |
| ElizaOS | Preview | MCP fallback |
| Plain HTTP/REST | GA | anything that speaks HTTP |

## Repos

| Repo | What it does | Install |
|---|---|---|
| [agentkit-actions](https://github.com/Floe-Labs/agentkit-actions) | TypeScript SDK — wallet, x402 payments, spend controls, agent awareness | `npm install floe-agent` |
| [agentkit-actions-py](https://github.com/Floe-Labs/agentkit-actions-py) | Python SDK — full parity | `pip install floe-agentkit-actions` |
| [floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server) | MCP server for Claude, Cursor, any MCP agent | [Setup](https://github.com/Floe-Labs/floe-mcp-server#readme) |
| [floe-cookbook](https://github.com/Floe-Labs/floe-cookbook) | Runnable end-to-end agents | `git clone` |

## Roadmap

Floe is shipping the spend layer first, and building the credit layer on top of it.

- **Working capital / credit lines** — *in development.* Borrow against deposits and, later, against your agent's usage and receivables.
- **Portable credit & trust record** — *in development.* Every transaction builds the behavioral data that will let agents be underwritten without re-running diligence.

Want early access to credit features? [Talk to us →](mailto:hello@floelabs.xyz)

---

Built by operators from Airwallex, Western Union, eBay, Kado, Transak.
[hello@floelabs.xyz](mailto:hello@floelabs.xyz)
