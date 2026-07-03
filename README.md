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

You should see `ac2-channel`. Try:

```text
Pair my AC2 wallet.
```

The plugin launches its MCP server through the published npm package `@goplausible/ac2-plugin-codex`.
