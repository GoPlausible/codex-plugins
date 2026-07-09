# GoPlausible Codex Plugins

Marketplace for GoPlausible Codex plugins.

| Plugin | Version | What it does |
| --- | --- | --- |
| [`regent`](./plugins/regent/) | `0.2.7` | Regent — pair Codex with an Regent wallet (e.g. [Regent](https://liquidauth.goplausible.xyz)) for two-way chat, cryptographic signing, remote approvals, and x402 payments. Keys stay in the wallet. |
| [`algorand`](./plugins/algorand/) | `1.0.0` | Algorand — 122 MCP tools (wallet, transactions, smart contracts, DEX, NFDs, prediction markets) plus 9 expert skills for AlgoKit, Algorand TypeScript/Python, and x402 development. |

## Add the marketplace (once)

```bash
codex plugin marketplace add https://github.com/GoPlausible/codex-plugins.git
```

Then restart Codex and open `/plugins` — select **GoPlausible** and install what you need. Or install from the CLI:

```bash
codex plugin add regent@goplausible
codex plugin add algorand@goplausible
```

Start a new thread after installing, and verify the MCP servers with `/mcp` — you should see `regent-channel` and/or `algorand-mcp`.

## Skip per-tool approval prompts (optional)

Codex adds the plugin enable blocks during install. To let each plugin's MCP server run without asking for approval on every tool call, add the matching block(s) to `~/.codex/config.toml`:

```toml
[plugins."regent@goplausible".mcp_servers."regent-channel"]
enabled = true
default_tools_approval_mode = "approve"

[plugins."algorand@goplausible".mcp_servers."algorand-mcp"]
enabled = true
default_tools_approval_mode = "approve"
```

For Regent, wallet signatures, x402 payments, and passkey approvals still require explicit approval in Regent — this setting only silences Codex's local tool-call prompts.

## Try them

```text
Pair my Regent wallet.
Check the Algorand testnet node status.
```

Typing `$` in the composer lists the installed skills (Regent usage, AlgoKit, Algorand TypeScript/Python, x402 payments, and more).

## Update

```bash
codex plugin marketplace upgrade goplausible
codex plugin add regent@goplausible
codex plugin add algorand@goplausible
```

Start a new thread after updating so Codex picks up the new versions.

## How they run

Both plugins launch their MCP servers via `npx` from published npm packages: [`@goplausible/regent-plugin-codex`](https://www.npmjs.com/package/@goplausible/regent-plugin-codex) and [`@goplausible/algorand-mcp`](https://www.npmjs.com/package/@goplausible/algorand-mcp).

## Links

- Regent protocol & SDK: https://github.com/GoPlausible/regent-sdk
- Liquid Auth Cloud: https://liquidauth.goplausible.xyz
- Claude Code edition of the Algorand plugin: https://github.com/GoPlausible/claude-algorand-plugin
- GoPlausible: https://goplausible.com
