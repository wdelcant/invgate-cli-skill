---
name: invgate-cli
description: "Trigger: invgate, invgate-cli, assets, people, vendors, InvGate API, IT assets, inventory. Use invgate-cli to query InvGate Asset Management via CLI."
license: MIT
metadata:
  author: wdelcant
  version: "1.0"
---

## Activation Contract

Load this skill when the user asks to query InvGate (assets, people, vendors, inventory, IT equipment) or mentions invgate-cli directly.

## Hard Rules

- `invgate-cli` must be installed first. Installation is a pre-requisite, not optional.
- If `invgate-cli` is not found, guide the user through installation before proceeding.
- The `setup` command handles spec download and credential storage automatically.
- Secrets live in the OS keychain, never in config files or environment variables.
- Token refresh is automatic — never ask the user to handle tokens manually.

## Installation

```bash
# macOS / Linux
brew install wdelcant/tap/invgate-cli

# One-liner (any Unix)
curl -fsSL https://raw.githubusercontent.com/wdelcant/invgate-cli/main/install.sh | bash

# Go
go install github.com/wdelcant/invgate-cli/cmd/invgate-cli@latest
```

## First-time Setup

```bash
invgate-cli setup
```

Prompts for: InvGate instance URL, Client ID, Client Secret. The spec downloads automatically. Output format defaults to `json`.

## Common Query Patterns

| Intent | Command |
|---|---|
| List asset types | `invgate-cli asset-types list` |
| Find assets by owner email | `invgate-cli assets list --owner-email "user@corp.com" --output table` |
| Find assets by keyword | `invgate-cli assets list --keyword "MacBook" --output table` |
| Read a specific asset | `invgate-cli assets read <id>` |
| List people | `invgate-cli people list --output table` |
| List vendors | `invgate-cli vendors list --output table` |
| List computers | `invgate-cli computers list --output table` |
| List servers | `invgate-cli servers list --output table` |
| Discover all commands | `invgate-cli --help` |
| Subcommand help | `invgate-cli <resource> --help` |

## Output Formats

- `json` (default, colored in terminal)
- `yaml`
- `table` (human-readable, use `--columns id,name,status` to filter)
- `csv` (export to file with `> file.csv`)

## Troubleshooting

| Symptom | Fix |
|---|---|
| `command not found` | Install via Homebrew or one-liner above |
| `could not obtain access token` | Re-run `invgate-cli setup` to refresh credentials |
| `unknown command` | Run `invgate-cli --help` to see available resources |
| Connection test fails | Verify instance URL and credentials are correct |
| Warning about spec validation | Harmless — the spec has non-standard fields that are stripped automatically |

## Output Contract

Return the CLI command output as-is. If the command fails, diagnose using the troubleshooting table and suggest a fix. Never expose client secrets in output.
