# @goplausible/regent-plugin-codex

Regent plugin for **Codex**. It pairs Codex with a Regent wallet such as
[Regent](https://liquidauth.goplausible.xyz/download/regent.apk) so you can
chat with your agent from your phone, approve what it does, sign with your
own keys, and pay for x402 resources — while the wallet keeps custody of
every key.

## What is Regent?

Regent (Agent-Controller Communication) is GoPlausible's open protocol
connecting AI agents to user-controlled wallets over an end-to-end encrypted,
peer-to-peer link (Liquid Auth / FIDO2 pairing + WebRTC DataChannels). The
agent never sees a private key: every signature and payment is approved by
the user in their wallet with a passkey or biometric. The same protocol
powers the Regent plugins for Claude Code and OpenClaw — this package brings it
to Codex.

## Features

- **Two-way chat with your agent from Regent** — send messages, images, and
  files from your phone; get replies, live activity status, and token usage.
- **Remote approvals** — when Codex wants to run a command or change files,
  the approval prompt arrives in your wallet chat; reply yes/no from the phone.
- **Cryptographic signing** with `regent_sign` — messages, typed data, and
  transactions across Algorand, EVM, and Solana; verified locally with the
  `regent_verify_*` tools.
- **Capability discovery** with `regent_capabilities` — identities, accounts,
  and what the connected wallet can sign.
- **x402 paid HTTP resources** — discover payment requirements, browse the
  Bazaar directory, and pay per-request from your wallet with
  `make_http_request_with_x402_regent`.
- **Slash commands everywhere** — the same `/regent …` command set as the Claude
  and OpenClaw plugins, plus `/skill` search over all installed Codex skills
  (with autocomplete in Regent) and direct `/<skill-name>` invocation.

## Requirements

- Node 20+ and the Codex CLI (or desktop app) with plugin support.
- a regent wallet such as Regent on your phone.

## Install

From the GoPlausible plugin marketplace:

```bash
codex plugin marketplace add https://github.com/GoPlausible/codex-plugins.git
codex plugin add regent@goplausible
```

Codex adds the plugin enable block during install. To let the Regent MCP server
run without asking for approval on every Regent tool call, add only this block to
`~/.codex/config.toml`:

```toml
[plugins."regent@goplausible".mcp_servers."regent-channel"]
enabled = true
default_tools_approval_mode = "approve"
```

Wallet signatures, x402 payments, and passkey approvals still require explicit
approval in Regent.

Then start a new Codex thread and pair your wallet:

```
Pair my Regent wallet.
```

Codex shows a QR code and deep link — scan it with Regent (or open the link
on your phone) and approve with your passkey. Pairing persists; future
sessions reconnect automatically with no QR.

## Update

```bash
codex plugin marketplace upgrade goplausible
codex plugin add regent@goplausible
```

Start a new thread after updating so Codex picks up the new version.

## Use

From the **terminal side**, just ask Codex naturally:

- "What's my wallet status?" / "Show my wallet capabilities."
- "Sign this message with my wallet." — Regent shows the approval modal.
- "Fetch this x402 resource and pay for it." — payment is approved in-wallet.

From **Regent**, chat with your Codex agent directly. Available commands
(type `/` for autocomplete):

- `/regent` — list Regent commands (`status`, `capabilities`, `version`, `forget`)
- `/skill <name> [args]` — search and run any installed Codex skill
- `/<skill-name> [args]` — run a skill directly, same as Codex's `$` style
- `/clear` — start a fresh conversation

Signing, x402 payments, approvals, images, and file attachments all work
from the wallet chat as well.

## Environment

| Variable | Purpose |
|---|---|
| `REGENT_LIQUID_AUTH_SERVER` | Override the Liquid Auth relay (default: GoPlausible's) |
| `REGENT_STATE_DIR` | Override the state directory (default `~/.codex/regent/`) |
| `REGENT_AGENT_DID` | Override the agent's DID |
| `REGENT_RTC_CONFIG` | Custom WebRTC configuration (JSON) |

## Links

- Regent SDK & protocol: https://github.com/GoPlausible/regent-sdk
- Regent wallet: https://liquidauth.goplausible.xyz/download/regent.apk
- GoPlausible: https://goplausible.com

Apache-2.0 © GoPlausible
