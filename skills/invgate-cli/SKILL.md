---
name: invgate-cli
description: "Trigger: invgate, invgate-cli, assets, people, vendors, InvGate API, IT assets, inventory. Use invgate-cli to query InvGate Asset Management via CLI."
license: MIT
metadata:
  author: wdelcant
  version: "1.1"
---

## Activation Contract

Load this skill when the user asks to query InvGate (assets, people, vendors, inventory, IT equipment) or mentions invgate-cli directly.

## Hard Rules

- `invgate-cli` must be installed first. Installation is a pre-requisite, not optional.
- If `invgate-cli` is not found, guide the user through installation before proceeding.
- The `setup` command handles spec download and credential storage automatically.
- Secrets live in the OS keychain (macOS/Windows) or a restricted file (Linux fallback).
- Token refresh is automatic — never ask the user to handle tokens manually.

## Installation

```bash
# Any OS (recommended)
npm install -g invgate-cli@latest

# macOS / Linux
brew install wdelcant/tap/invgate-cli

# Windows
scoop bucket add invgate https://github.com/wdelcant/scoop-bucket
scoop install invgate-cli

# Go developers
go install github.com/wdelcant/invgate-cli/cmd/invgate-cli@latest
```

## First-time Setup

```bash
invgate-cli setup
```

Prompts for: InvGate instance URL, Client ID, Client Secret (hidden input). The spec downloads automatically.

## Common Query Patterns

| Intent | Command |
|---|---|
| List asset types | `invgate-cli asset-types list` |
| Find assets by owner email | `invgate-cli assets list --owner-email "user@corp.com" --output table` |
| Find assets by keyword/serial | `invgate-cli assets list --keyword "MacBook" --output table` |
| Read a specific asset | `invgate-cli assets read <id>` |
| List people | `invgate-cli people list --output table` |
| List vendors | `invgate-cli vendors list --output table` |
| List computers | `invgate-cli computers list --output table` |
| Paginate results | `invgate-cli assets list --page 2 --output table` |
| Discover all commands | `invgate-cli --help` |

## Output Formats

- `json` (default, colored in terminal)
- `yaml`
- `table` (human-readable, clean column alignment)
- `csv` (export with `> file.csv`)
- `record` (vertical key:value per record — best for wide data)

## Troubleshooting

| Symptom | Fix |
|---|---|
| `command not found` | Install via npm or brew above |
| `could not obtain access token` | Re-run `invgate-cli setup` to refresh credentials |
| `unknown command` | Run `invgate-cli --help` to see available resources |
| Connection test fails | Verify instance URL and credentials are correct |
| Credentials lost after 24h | Re-run `invgate-cli setup` (file fallback on headless Linux) |

## Output Contract

Return the CLI command output as-is. If the command fails, diagnose using the troubleshooting table and suggest a fix. Never expose client secrets in output.
