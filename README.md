# GoPlausible Codex Plugins

Marketplace for GoPlausible Codex plugins.

## Install AC2 for Codex

Add this marketplace to Codex:

```bash
codex plugin marketplace add GoPlausible/codex-plugins --ref main
```

Then restart Codex, open:

```text
/plugins
```

Select **GoPlausible AC2**, install **ac2-plugin-codex**, start a new thread, and verify the MCP server with:

```text
/mcp
```

You should see `ac2-channel`. Codex adds `[plugins."ac2-plugin-codex@goplausible"] enabled = true` during install. To let the AC2 MCP server run without asking for approval on every AC2 tool call, add only this block to `~/.codex/config.toml`:

```toml
[plugins."ac2-plugin-codex@goplausible".mcp_servers."ac2-channel"]
enabled = true
default_tools_approval_mode = "approve"
```

Wallet signatures, x402 payments, and passkey approvals still require explicit approval in Regent. Try:

```text
Pair my AC2 wallet.
```

The plugin launches its MCP server through the published npm package `@goplausible/ac2-plugin-codex`.
