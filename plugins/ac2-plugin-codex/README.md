# @goplausible/ac2-plugin-codex

AC2 plugin for **Codex**. It pairs Codex with an AC2 wallet such as
[Regent](https://liquidauth.goplausible.xyz/download/regent.apk) over Liquid
Auth (FIDO2) + WebRTC DataChannels.

The plugin exposes the same AC2 tool surface as the Claude and OpenClaw
packages:

- **Wallet pairing** with `ac2_pair`, `ac2_status`, and `ac2_forget`.
- **Cryptographic signing** with `ac2_sign`; the wallet holds the keys and the
  user approves in-wallet with passkey or biometric.
- **Local verification** with `ac2_verify_*` tools for raw, message, typed-data,
  and transaction signatures across Algorand, EVM, and Solana.
- **Capability discovery** with `ac2_capabilities`.
- **x402 paid HTTP resources** with `make_http_request_with_x402_ac2`,
  `x402_discover_payment_requirements_ac2`, and the Bazaar discovery tools.

## Requirements

- Node 20+.
- An AC2 wallet such as Regent.
- Codex with local plugin support.

## Codex Plugin Contents

- `.codex-plugin/plugin.json` - Codex plugin manifest.
- `.mcp.json` - MCP server registration for `ac2-channel`.
- `server.ts` and `src/` - AC2 MCP server and shared protocol tooling.
- `skills/ac2/SKILL.md` - agent instructions for using AC2 signing and x402.
- `commands/` - command prompts matching the Claude plugin command surface.
- `hooks/hooks.json` - hook bridge payloads matching the existing AC2 channel
  implementation.

## Build

```bash
npm run build
```

`build.mjs` bundles `server.ts` and the pure-JS dependencies into
`dist/server.js`. The only runtime dependency left external is `@roamhq/wrtc`,
because it is a native WebRTC addon.

## Local Development

From this package:

```bash
npm install
npm run build
```

The Codex manifest points at `.mcp.json`, whose MCP server launches the package
through:

```bash
npx @goplausible/ac2-plugin-codex@0.1.0
```

During local development you can run the server directly:

```bash
npm run start
```

Then use the exposed MCP tools:

- `ac2_pair` - show a QR code and Liquid Auth deep link for wallet pairing.
- `ac2_status` - inspect pairing and WebRTC connection state.
- `ac2_capabilities` - list wallet identities and accounts.
- `ac2_sign` - request a wallet signature.
- `ac2_verify_*` - verify signatures locally.
- `ac2_forget` - remove the active pairing.
- `ac2_version` - show plugin and bundled SDK versions.

State is stored under `~/.codex/ac2/`.
