<p align="center"><img src="https://raw.githubusercontent.com/Floe-Labs/.github/main/profile/banner.png" alt="Floe Labs" width="100%" /></p>

# Floe Labs

**Spend controls for Voice AI.** Your agent's whole bill — telephony, STT, LLM, TTS, search — on one ledger, enforced before money moves. Inside Vapi, Retell & Bland, or fully BYOK.

[Website](https://floelabs.xyz) · [Docs](https://floe-labs.gitbook.io/docs) · [Dashboard](https://dev-dashboard.floelabs.xyz) · [𝕏 @FloeLabs](https://x.com/FloeLabs)

[![npm](https://img.shields.io/npm/v/floe-agent?label=npm&color=green)](https://www.npmjs.com/package/floe-agent)
[![pypi](https://img.shields.io/pypi/v/floe-agentkit-actions?label=pypi&color=blue)](https://pypi.org/project/floe-agentkit-actions/)
[![license](https://img.shields.io/badge/license-MIT-brightgreen)](https://github.com/Floe-Labs/agentkit-actions/blob/main/LICENSE)

---

> **Start free.** $3 Welcome Credit — 300 API credits on signup, no card required.
> Your agent makes its first paid call in minutes. [Get started →](https://dev-dashboard.floelabs.xyz)

## The problem

A voice call touches 7–20 vendors, each billing separately. Token and TTS usage varies every conversation, so true per-call cost only exists by joining usage data across providers after the call. A token router meters ~40% of the bill — the LLM slice — and is blind to the other 60%. On BYOK, platform dashboards report provider costs as $0.

Floe is that join, plus enforcement: per-call cost across every vendor, and caps applied **before** money moves where Floe is in the path — with a between-call circuit breaker everywhere else. Gateway overhead: **38ms p50 / ~180ms p99** on live keyless production traffic.

## Quickstart — one voice turn, one budget

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

All three legs share `X-Floe-Task-Id`, so one budget caps the whole conversation — STT, LLM, and TTS together, on one ledger. Each response returns its cost in `X-Floe-Payment-Amount` (e.g. `0.0125`).

**MCP (zero install)** — add to Claude Code / Cursor / Claude Desktop:

```bash
claude mcp add --transport http floe https://mcp.floelabs.xyz/mcp \
  --header "Authorization: Bearer YOUR_FLOE_KEY"
```

Prefer an SDK? `npm install floe-agent` or `pip install floe-agentkit-actions` — see [Repos](#repos).

## Three ways in

**1 · Inside your platform (Vapi / Retell / Bland).** Documented hooks, zero platform cooperation:

- **Custom-LLM slot → Floe** — pre-call enforcement on ~60% of call cost. Recipes: [vapi-custom-llm](https://github.com/Floe-Labs/floe-cookbook/tree/main/vapi-custom-llm), [retell-custom-llm](https://github.com/Floe-Labs/floe-cookbook/tree/main/retell-custom-llm). *(Bland has no self-serve custom LLM — govern it with Reconcile Mode below.)*
- **Custom voice & transcriber → Floe** *(early access)* — metered STT/TTS in your provider dropdown. Behind a flag until we publish a media-path latency benchmark — we don't promote a leg in your audio path ahead of its numbers. Recipe: [vapi-voice-metered](https://github.com/Floe-Labs/floe-cookbook/tree/main/vapi-voice-metered).
- **End-of-call webhooks → Reconcile Mode** — every call reconciled onto one ledger at call-end; cross your cap and the next call is denied. A runaway campaign dies at call N, not call 10,000.
- **Coverage Score**, per agent, in the dashboard — % of spend enforceable pre-call vs reconciled vs dark, and which leg to move to raise it.

Pre-call where we're in the path. Circuit breaker everywhere else. [Setup →](https://floe-labs.gitbook.io/docs/the-voice-stack/voice-orchestrators) · [Graduate to 100% coverage →](https://floe-labs.gitbook.io/docs/the-voice-stack/migrate-to-full-coverage)

**2 · BYOK.** Keep your vendor accounts and keys — Floe meters, joins, and caps on top. Route just the LLM leg by changing the base URL and key:

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://credit-api.floelabs.xyz/v1",  # was https://api.openai.com/v1
    api_key=os.environ["FLOE_API_KEY"],             # your Floe key — not an OpenAI key
)
# every call now bills to your Floe balance, under your spend caps
```

OpenAI-compatible, so it works from any SDK. → [Add Floe to your existing pipeline](https://floe-labs.gitbook.io/docs/getting-started/integrate-existing-pipeline)

**3 · Keyless.** One Floe key, no per-vendor accounts, welcome credits. Fund by card; settlement is automatic. Best for prototypes and net-new agents.

## Vendor Marketplace — 2,000+ vendor API services, one key

| Category | Services |
|---|---|
| Compute | Venice AI · OpenAI · Anthropic · Google Gemini · z.ai · Kimi |
| Voice | Deepgram · ElevenLabs · Venice AI · Floe Phone via Twilio (live) |
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
| [agentkit-actions](https://github.com/Floe-Labs/agentkit-actions) | TypeScript SDK — spend controls, metered vendor calls, agent awareness | `npm install floe-agent` |
| [agentkit-actions-py](https://github.com/Floe-Labs/agentkit-actions-py) | Python SDK — full parity | `pip install floe-agentkit-actions` |
| [floe-guard](https://github.com/Floe-Labs/floe-guard) | Local budget guardrail — hard-stops a runaway agent before it overspends | `pip install floe-guard` |
| [floe-cookbook](https://github.com/Floe-Labs/floe-cookbook) | Runnable end-to-end agents, including voice | `git clone` |
| [floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server) | MCP server for Claude, Cursor, any MCP agent | [Setup](https://github.com/Floe-Labs/floe-mcp-server#readme) |
| [eve-floe](https://github.com/Floe-Labs/eve-floe) | Reference voice agent built on Floe | `git clone` |

**Voice recipes** (in [floe-cookbook](https://github.com/Floe-Labs/floe-cookbook)): [vapi-custom-llm](https://github.com/Floe-Labs/floe-cookbook/tree/main/vapi-custom-llm) · [retell-custom-llm](https://github.com/Floe-Labs/floe-cookbook/tree/main/retell-custom-llm) · [vapi-voice-metered](https://github.com/Floe-Labs/floe-cookbook/tree/main/vapi-voice-metered)

---

Built by operators from Airwallex, Western Union, eBay, Kado, Transak.
[hello@floelabs.xyz](mailto:hello@floelabs.xyz)
