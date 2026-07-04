# codex-plugin-algorand

Algorand blockchain integration for **Codex**, by GoPlausible. One install gives
Codex the full Algorand stack:

- **122 MCP tools** via the [Algorand MCP server](https://www.npmjs.com/package/@goplausible/algorand-mcp) —
  wallet management, ALGO/ASA payments, asset & application transactions,
  atomic groups, TEAL compile/disassemble, indexer queries, NFDs, Tinyman &
  Haystack DEX swaps, Alpha Arcade prediction markets, Pera verification, and
  x402 paid-HTTP tools.
- **9 expert skills** (surface as `$` entries in Codex):
  - `algorand-development` — AlgoKit projects, ARC standards, troubleshooting
  - `algorand-typescript` / `algorand-python` — PuyaTs / PuyaPy smart contracts
  - `algorand-interaction` — on-chain workflows via the MCP tools
  - `algorand-x402-payment` — pay for 402-protected APIs at runtime
  - `algorand-x402-typescript` / `algorand-x402-python` — build x402 apps
  - `alpha-arcade-interaction` — prediction-market trading
  - `haystack-router-interaction` — best-price DEX routing

When any HTTP request returns **402 Payment Required**, the x402-payment skill
takes over and pays for the resource from the configured wallet — per request,
with spend caps.

## Requirements

- Codex CLI or desktop app with plugin support · Node 20+
- For wallet operations: an Algorand account (mnemonic via the MCP server's
  environment, or use it read-only without one)

## Install

```bash
# one-time: add the marketplace
codex plugin marketplace add https://github.com/GoPlausible/codex-plugins.git
# install
codex plugin add codex-plugin-algorand@goplausible
```

To let the Algorand MCP server run without approval prompts on every tool
call, add this block to `~/.codex/config.toml`:

```toml
[plugins."codex-plugin-algorand@goplausible".mcp_servers."algorand-mcp"]
enabled = true
default_tools_approval_mode = "approve"
```

Start a new Codex thread after installing.

## Update

```bash
codex plugin marketplace upgrade
codex plugin add codex-plugin-algorand@goplausible
```

Start a new thread after updating so Codex picks up the new version.

## Use

Ask naturally — "check my wallet balance", "swap 10 ALGO to USDC at the best
price", "create an AlgoKit TypeScript project", "fetch this paid API" — or
invoke a skill directly with `$` (e.g. `$algorand-development`).

## Links

- Algorand MCP: https://github.com/GoPlausible/algorand-mcp
- Claude Code edition of this plugin: https://github.com/GoPlausible/claude-algorand-plugin
- GoPlausible: https://goplausible.com

MIT © GoPlausible
