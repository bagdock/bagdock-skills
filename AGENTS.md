# Bagdock Agent Skills

This repository contains skills for AI coding agents that work with the Bagdock platform.

## Quick setup

### Codex / Conductor

```bash
claude mcp add bagdock -s user -- npx -y bagdock-mcp
```

### Environment

Set your API key:

```bash
export BAGDOCK_API_KEY=bdok_sk_your_key_here
```

## Available skills

- `skills/bagdock/` — Bagdock platform API (apps, edges, auth, marketplace)
- `skills/bagdock-cli/` — CLI tool reference (deploy, submit, env, keys)

## Conventions

- All Bagdock API keys start with `bdok_sk_` (secret) or `bdok_pk_` (publishable)
- The CLI outputs JSON when piped or when `--json` is passed
- Exit code 0 = success, 1 = error
- Errors always include `code` and `message` fields
