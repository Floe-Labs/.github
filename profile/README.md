<p align="center"><img src="https://raw.githubusercontent.com/Floe-Labs/.github/main/profile/banner.png" alt="Floe Labs" width="100%" /></p>

# Floe Labs

**Trusted settlement for task-based AI.** Your AI vendor counts resolutions, then sends an invoice. Floe reconciles every AI task and outcome you're billed for against your own tickets, helpdesk and CRM, codes each one, and signs the statement — so you know your AI outcomes before the QBR, the CFO or the renewal asks.

[Website](https://www.floefinance.com/) · [AI buyers](https://www.floefinance.com/aibuyers) · [Cleared Work Taxonomy](https://www.floefinance.com/taxonomy) · [Docs](https://floe-labs.gitbook.io/docs) · [Dashboard](https://dev-dashboard.floelabs.xyz) · [𝕏 @FloeLabs](https://x.com/FloeLabs)

---

## The price per resolution is the definition you're paying for

Today every AI vendor decides what counts as a billable task or outcome.

| Vendor | Billed as resolved when… | Price per resolution |
|---|---|---|
| Fin | The customer confirms, or leaves without asking for more help (an "assumed" resolution). Still charged if a teammate joins after Fin answered, unless the customer asked for help. | $0.99 |
| Zendesk | Zendesk's own AI check marks the resolution "Verified." | $1.50 committed · $2.00 pay-as-you-go |
| HubSpot | The agent handled the conversation and it wasn't handed to a human within 72 hours. | $0.50 |
| Salesforce Help Agent | The issue is resolved end to end. Not charged if the customer asks for a human or leaves negative feedback. | $2.00 |

Vendors' published terms and reported prices, checked October 2026. Any contract with a countable unit and an invoice fits: per resolved conversation, per verified resolution, per finalized clinical note, per pull-request-ready task.

## What Floe finds

- **Invoice errors** — billed, but not in your records.
- **Invalid outcomes** — resolutions your team had to finish.
- **Value leakage** — credits you were owed, minimums you didn't use.
- **Renewal leverage** — what to commit to next year.

## The output

Four numbers and one dispute file. Every number carries its outcome IDs.

| | |
|---|---|
| **$ recoverable** | invoice errors and credits |
| **$ / outcome** | what the contract says you paid per unit |
| **$ / valid outcome** | what you paid per unit that counted |
| **% failed** | paid outcomes that failed your standard |

> Vendor: "We delivered 100,000 resolutions."
> Finance: "These were reopened and closed by my team. These have no ticket. Here are the IDs. You billed us for 100,000. 73,400 satisfied our definition. 4,600 don't satisfy the contract; we're disputing those. The other 22,000 get repriced at renewal."

## The Cleared Work Taxonomy

Every billed task or outcome gets a code and one of six actions — **accept**, **credit**, **unbilled**, **dispute**, **renewal lever**, **identify**. Match first; an amount counts once. A code never changes meaning: new meaning, new code. Buyer-only findings (definitional drift) never reach the vendor. No model in the math.

→ [Floe Cleared Work Taxonomy v1.2](https://www.floefinance.com/taxonomy)

## How it runs

Five read-only inputs: the contract or order form, the vendor's event logs or usage reports, the invoices, an export from your own system of record (helpdesk, CRM, claims, contact center), and your outcome rules. Nothing is written back to any system. One vendor, 30 days, walk away.

| | |
|---|---|
| **Contingency audit** | 20% of recovered credits. Nothing found, nothing owed. |
| **Per-vendor audit** | Fixed fee on request. Credited against a ledger subscription if you continue. |

→ [Start an audit](https://www.floefinance.com/aibuyers)

## For AI vendors

Add Floe Cleared Work to your invoices: publish the task or outcome definition; emit one event per outcome with a stable ID and negate reversals, cancels and retries; stamp the buyer's key on every billed event; measure minimums against delivered units; bill the order-form rate per outcome type and channel; open the event log for the period and leave a dispute window long enough to recount.

## Open source

Floe's agent-billing tools — metering, budgets, keys — are open source and maintained.

| Repo | Role | Install |
|---|---|---|
| [floe-guard](https://github.com/Floe-Labs/floe-guard) | Local spend meter and budget gate for AI tasks. MIT, no account. | `pip install floe-guard` |
| [floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server) | Floe over MCP, for Claude, Cursor, and any MCP client. | [Setup](https://github.com/Floe-Labs/floe-mcp-server#readme) |
| [agent-skills](https://github.com/Floe-Labs/agent-skills) | Agent skills that teach a coding agent to set up and use Floe. | `npx skills add floe-labs/agent-skills` |
| [floe-cookbook](https://github.com/Floe-Labs/floe-cookbook) | Runnable examples and reference agents. | `git clone` |
| [pipecat-floe](https://github.com/Floe-Labs/pipecat-floe) | Pipecat voice plugin metered on Floe. Maintenance mode. | `pip install pipecat-floe` |
| [livekit-plugins-floe](https://github.com/Floe-Labs/livekit-plugins-floe) | LiveKit Agents plugin metered on Floe. Maintenance mode. | `pip install livekit-plugins-floe-v1` |

---

Built by operators from Airwallex, Western Union, eBay, Kado, Transak.
[hello@floefinance.com](mailto:hello@floefinance.com)
