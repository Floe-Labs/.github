<p align="center"><img src="https://raw.githubusercontent.com/Floe-Labs/.github/main/profile/banner.png" alt="Floe Labs" width="100%" /></p>

# Floe Labs

**The AI Initiative Ledger — where the AI money is going, and whether it is working.** One ledger for the head of finance who has to defend the AI line item. Every AI initiative holds its cost entries and its value entries, and every number carries a source, a confidence grade (A–D), and a deterministic formula. Periods lock; restatements are journaled.

[Website](https://www.floefinance.com/) · [Docs](https://floe-labs.gitbook.io/docs) · [Dashboard](https://dev-dashboard.floelabs.xyz) · [𝕏 @FloeLabs](https://x.com/FloeLabs)

[![floe-guard](https://img.shields.io/pypi/v/floe-guard?label=floe-guard&color=blue)](https://pypi.org/project/floe-guard/)
[![@floelabs/cli](https://img.shields.io/npm/v/@floelabs/cli?label=%40floelabs%2Fcli&color=green)](https://www.npmjs.com/package/@floelabs/cli)
[![license](https://img.shields.io/badge/license-MIT-brightgreen)](https://github.com/Floe-Labs/floe-guard/blob/main/LICENSE)

---

> **Start free.** $3 Welcome Credit — 300 API credits on signup, no card required. [Get started →](https://dev-dashboard.floelabs.xyz)

## The problem

AI spend lands across a dozen vendors — models, speech, telephony, tools, infrastructure. Those bills arrive separately, in different units, on different days, and your finance team spends weeks stitching them together. At the end, the questions a head of finance gets asked are still open: **what does this AI initiative cost, what did it produce, and how sure are we of each number?**

Floe is the accounting layer for that line item. It puts the cost of an initiative next to what the initiative produced, and it says how much each number can be trusted.

## The ledger

| | |
|---|---|
| **Initiatives** | Each AI initiative is one record. It holds its cost entries and its value entries side by side. |
| **Source** | Every number says where it came from. |
| **Confidence grade** | Every number carries a grade from A to D, so a figure tied to a vendor's own record is never read the same way as an estimate. |
| **Deterministic formula** | Every derived number comes from a fixed formula. Same inputs, same result. |
| **Period lock** | A closed period stays closed. Corrections are journaled as restatements, not edited in place. |

Where an outcome exists, the ledger joins the cost to it. Where one doesn't, it says so.

## How cost gets into the ledger

**1 · Through the gateway.** Route a model call through Floe by changing the base URL and key. The call is metered, tagged, and held to your spend caps:

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://credit-api.floelabs.xyz/v1",  # was https://api.openai.com/v1
    api_key=os.environ["FLOE_API_KEY"],             # your Floe key — not an OpenAI key
)
# every call now bills to your Floe balance, under your spend caps
```

OpenAI-compatible, so it works from any SDK. Keep your own vendor accounts and keys (BYOK), or use one Floe key with no per-vendor accounts (keyless). Gateway overhead: **38ms p50 / ~180ms p99** on live keyless production traffic. → [Add Floe to your existing pipeline](https://floe-labs.gitbook.io/docs/start-here/integrate-existing-pipeline)

**2 · From the vendor's own records.** Give Floe read-only billing access to a vendor and it reconciles your costs against that vendor's records. → [Vendor actuals](https://floe-labs.gitbook.io/docs/know-your-costs/vendor-actuals) · [Vendor connections](https://floe-labs.gitbook.io/docs/know-your-costs/vendor-connections)

**3 · From a local meter.** [`floe-guard`](https://github.com/Floe-Labs/floe-guard) meters and caps spend inside your own process, with no telemetry by default. Ledger sync (rolling out) pushes its priced spend events to Floe — opt-in, no prompts, no content. → [Ledger sync](https://floe-labs.gitbook.io/docs/connect-your-stack/ledger-sync)

**4 · From voice platforms.** Voice is one cost source among the others. Vapi, Retell, and Bland connect through their own documented hooks — the custom-LLM slot where the platform has one, and end-of-call webhooks. Pipecat and LiveKit connect through the plugins below. → [Setup](https://floe-labs.gitbook.io/docs/connect-your-stack/voice-orchestrators)

**Coverage Score**, per agent, in the dashboard — the share of known spend Floe can enforce before the call, reconcile after it, or cannot see, and which leg to move to raise it. → [Coverage Score](https://floe-labs.gitbook.io/docs/know-your-costs/coverage-score)

## Quickstart

**MCP (zero install)** — add to Claude Code / Cursor / Claude Desktop:

```bash
claude mcp add --transport http floe https://mcp.floelabs.xyz/mcp \
  --header "Authorization: Bearer YOUR_FLOE_KEY"
```

**CLI** — onboard from your terminal:

```bash
npx @floelabs/cli init
```

## Repos

| Repo | Role | Install |
|---|---|---|
| [floe-guard](https://github.com/Floe-Labs/floe-guard) | Local spend meter and budget gate. Runs in your process and feeds the ledger through ledger sync. | `pip install floe-guard` |
| [floe-cli](https://github.com/Floe-Labs/floe-cli) | The platform from your terminal — agents, keys, budgets, billing. | `npx @floelabs/cli init` |
| [floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server) | The platform over MCP, for Claude, Cursor, and any MCP client. | [Setup](https://github.com/Floe-Labs/floe-mcp-server#readme) |
| [agent-skills](https://github.com/Floe-Labs/agent-skills) | Agent skills that teach a coding agent to set up and use Floe. | `npx skills add floe-labs/agent-skills` |
| [floe-cookbook](https://github.com/Floe-Labs/floe-cookbook) | Examples — runnable end-to-end agents, including voice. | `git clone` |
| [eve-floe](https://github.com/Floe-Labs/eve-floe) | Example — an Eve agent template with its API spend metered on Floe. | `git clone` |
| [pipecat-floe](https://github.com/Floe-Labs/pipecat-floe) | Voice cost source — Pipecat services metered on Floe. Maintenance mode. | `pip install pipecat-floe` |
| [livekit-plugins-floe](https://github.com/Floe-Labs/livekit-plugins-floe) | Voice cost source — LiveKit Agents plugin metered on Floe. Maintenance mode. | `pip install livekit-plugins-floe-v1` |
| [floe-labs-docs](https://github.com/Floe-Labs/floe-labs-docs) | Source for the documentation. | [Read the docs](https://floe-labs.gitbook.io/docs) |

---

Built by operators from Airwallex, Western Union, eBay, Kado, Transak.
[hello@floefinance.com](mailto:hello@floefinance.com)
