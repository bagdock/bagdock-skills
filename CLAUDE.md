# Bagdock Agent Skills

This repository contains skills for AI coding agents that work with the Bagdock platform.

## Quick setup

Add the Bagdock MCP server:

```bash
claude mcp add bagdock -s user -- npx -y bagdock-mcp
```

Set your API key:

```bash
export BAGDOCK_API_KEY=sk_live_your_key_here
```

## Available skills

- `skills/bagdock/` — Bagdock platform API (apps, edges, auth, marketplace)
- `skills/bagdock-cli/` — CLI tool reference (deploy, submit, env, keys)

## Conventions

- API keys use Stripe-style prefixes: `sk_live_` / `sk_test_` (secret), `pk_live_` / `pk_test_` (publishable)
- The CLI outputs JSON when piped or when `--json` is passed
- Exit code 0 = success, 1 = error
- Errors always include `code` and `message` fields
