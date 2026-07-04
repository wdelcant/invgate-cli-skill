# invgate-cli Skill

AI agent skill for [invgate-cli](https://github.com/wdelcant/invgate-cli) — the runtime OpenAPI/Swagger CLI for InvGate Asset Management.

## Install

```bash
npx skills add https://github.com/wdelcant/invgate-cli-skill --skill invgate-cli
```

## What it does

Guides AI agents on installing, configuring, and using `invgate-cli` to query InvGate's API. Triggers on: `invgate`, `assets`, `people`, `vendors`, `inventory`, `IT equipment`.

## Requirements

- [invgate-cli](https://github.com/wdelcant/invgate-cli) installed
- InvGate API credentials (Client ID + Client Secret)
