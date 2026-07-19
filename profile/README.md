<p align="center"><img src="https://raw.githubusercontent.com/Floe-Labs/.github/main/profile/banner.png" alt="Floe Labs" width="100%" /></p>

# Floe Labs

**One key for your voice agent's entire bill — LLM, voice, telephony, data.** One endpoint to pay across any LLM or voice vendor API services, with programmable, context-aware budgets. Walletless.

[Website](https://floelabs.xyz) · [Docs](https://floe-labs.gitbook.io/docs) · [Dashboard](https://dev-dashboard.floelabs.xyz) · [𝕏 @FloeLabs](https://x.com/FloeLabs)

[![npm](https://img.shields.io/npm/v/floe-agent?label=npm&color=green)](https://www.npmjs.com/package/floe-agent)
[![pypi](https://img.shields.io/pypi/v/floe-agentkit-actions?label=pypi&color=blue)](https://pypi.org/project/floe-agentkit-actions/)
[![license](https://img.shields.io/badge/license-MIT-brightgreen)](https://github.com/Floe-Labs/agentkit-actions/blob/main/LICENSE)

---

> **Start free.** 200 API credits on signup — no card, no wallet.
> Your agent makes its first paid API call in minutes. [Get started →](https://dev-dashboard.floelabs.xyz)

## Why Floe

**A token router meters your LLM spend — ~40% of a voice call. Floe meters 100%:** transcription, speech, telephony, search, and reasoning, on one key.

Your agent calls a dozen paid APIs — LLMs, voice, search, data. That's a dozen
accounts, a dozen prepaid balances, a dozen keys, and no unified way to see or
govern what your agent spends. Agents overspend, loop, and stall.

Floe gives your agent **a budget, not a balance**:

- **One endpoint, 2,000+ LLM inference + vendor API services.** Pay any vendor through Floe. No per-vendor accounts or keys.
- **Programmable spend controls.** Per-call caps, daily limits, allowed destinations — set at the vendor, agent, or team level, time-bound. Enforced *before* money moves.
- **Budget-aware routing.** Every response carries `result.budgetAdvisory` — how close the agent is to its tightest cap. Your agent reads it and downgrades, finishes the task, or hard-stops *before* it overspends, instead of failing at the cap.
- **Walletless.** Email + a funding source. We provision wallets in the background — no MetaMask, no seed phrase, no gas. The stablecoin rails are invisible.
- **Real-time visibility.** Every call is a typed receipt: target, amount, status, time. Reconcile, alert, or revoke from the dashboard.

## Quickstart — one voice turn, one key

A single spoken turn spends across speech-to-text, an LLM, and text-to-speech. Same key, same task budget for all three — a token router only ever sees the middle step.

```bash
# 1 · Transcribe (Deepgram) — through the Floe proxy
curl -X POST https://credit-api.floelabs.xyz/v1/proxy/fetch \
  -H "Authorization: Bearer $FLOE_API_KEY" \
  -H "Content-Type: application/json" \
  -H "X-Floe-Task-Id: call-8842" \
  -d '{"url":"<DEEPGRAM_STT_ENDPOINT>","method":"POST","body":"{...audio...}"}'

# 2 · Reason (any LLM) — keyless: only your Floe key, same ledger
curl -X POST https://credit-api.floelabs.xyz/v1/chat/completions \
  -H "Authorization: Bearer $FLOE_API_KEY" \
  -H "Content-Type: application/json" \
  -H "X-Floe-Task-Id: call-8842" \
  -d '{"model":"openai/gpt-4o","messages":[{"role":"user","content":"Book Friday at 2pm."}]}'

# 3 · Speak (ElevenLabs) — through the Floe proxy
curl -X POST https://credit-api.floelabs.xyz/v1/proxy/fetch \
  -H "Authorization: Bearer $FLOE_API_KEY" \
  -H "Content-Type: application/json" \
  -H "X-Floe-Task-Id: call-8842" \
  -d '{"url":"<ELEVENLABS_TTS_ENDPOINT>","method":"POST","body":"{...text...}"}'
```

All three legs share `X-Floe-Task-Id`, so one task budget caps the whole conversation — STT, LLM, and TTS together, on one ledger.

**MCP (zero install)** — add to Claude Desktop / Claude Code / Cursor:

```json
{ "mcpServers": { "floe": {
  "url": "https://mcp.floelabs.xyz/mcp",
  "transport": "streamable-http"
} } }
```

Prefer an SDK? `npm install floe-agent` or `pip install floe-agentkit-actions` — see [Repos](#repos).

→ [Voice Stack quickstart →](https://floe-labs.gitbook.io/docs/build/voice-stack)

## Vendor Marketplace — 2,000+ vendor API services, one key

| Category | Services |
|---|---|
| Compute | Venice AI · OpenAI · Anthropic · Google Gemini · z.ai · Kimi |
| Voice | Deepgram · ElevenLabs · Venice AI · Twilio (soon) |
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
| Plain HTTP/REST | GA | anything that speaks HTTP |

## Repos

| Repo | What it does | Install |
|---|---|---|
| [agentkit-actions](https://github.com/Floe-Labs/agentkit-actions) | TypeScript SDK — wallet, x402 payments, spend controls, agent awareness | `npm install floe-agent` |
| [agentkit-actions-py](https://github.com/Floe-Labs/agentkit-actions-py) | Python SDK — full parity | `pip install floe-agentkit-actions` |
| [floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server) | MCP server for Claude, Cursor, any MCP agent | [Setup](https://github.com/Floe-Labs/floe-mcp-server#readme) |
| [floe-cookbook](https://github.com/Floe-Labs/floe-cookbook) | Runnable end-to-end agents, including voice | `git clone` |
| [eve-floe](https://github.com/Floe-Labs/eve-floe) | Reference voice agent built on Floe | `git clone` |
| [floe-guard](https://github.com/Floe-Labs/floe-guard) | Local budget guardrail — hard-stops a runaway agent before it overspends | `pip install floe-guard` |

## Roadmap

Floe is shipping the spend layer first, and building the credit layer on top of it.

- **Working capital / credit lines** — *in development.* Borrow against deposits and, later, against your agent's usage and receivables.
- **Portable credit & trust record** — *in development.* Every transaction builds the behavioral data that will let agents be underwritten without re-running diligence.

Want early access to credit features? [Talk to us →](mailto:hello@floelabs.xyz)

---

Built by operators from Airwallex, Western Union, eBay, Kado, Transak.
[hello@floelabs.xyz](mailto:hello@floelabs.xyz)
