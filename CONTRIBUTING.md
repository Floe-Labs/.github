# Contributing to Floe Labs

Floe is spend controls for Voice AI. We build the wallet, payments, and credit
that let agents transact on their own.

This is the organization-wide contribution guide for
[Floe Labs](https://github.com/Floe-Labs). It applies to all Floe-Labs projects
that do not define their own `CONTRIBUTING.md`. A repository that ships its own
guide overrides this default.

## Where the projects live

Most contributions happen in our public repos:

- [agentkit-actions](https://github.com/Floe-Labs/agentkit-actions) — TypeScript AgentKit provider (`floe-agent` on npm).
- [agentkit-actions-py](https://github.com/Floe-Labs/agentkit-actions-py) — Python AgentKit provider (`floe-agentkit-actions` on PyPI).
- [floe-mcp-server](https://github.com/Floe-Labs/floe-mcp-server) — MCP server for Claude Desktop, Cursor, and other MCP clients.
- [floe-cookbook](https://github.com/Floe-Labs/floe-cookbook) — example agents and integrations.
- [floe-guard](https://github.com/Floe-Labs/floe-guard) — local budget guardrail for AI agents.

## Contribution flow

1. Fork the repo and create a feature branch off `main` (e.g. `feat/your-change`).
2. Make your change with tests, and keep the repo's checks green.
3. Open a **draft pull request** against `main` and describe what changed and why.
4. A maintainer will review. Address feedback, then mark the PR ready.

Open an issue first if you want to discuss a larger change before writing code.

## Code style

Each repo enforces its own linters and formatters — run them before pushing:

- **Python** projects use [`ruff`](https://docs.astral.sh/ruff/) for linting and
  formatting (`ruff check .` and `ruff format .`), with type hints throughout.
- **TypeScript** projects use the repo's own ESLint and Prettier config (typically
  `pnpm lint` and `pnpm typecheck`).

Check the target repo's `README.md` for its exact dev setup and commands.

## Be excellent

- Keep changes small and focused, with tests that describe behavior.
- Write clear PR descriptions — what changed, why, and how you verified it.
- No low-effort PRs (drive-by formatting, untested generated code, or churn).

Thanks for contributing to Floe Labs.
