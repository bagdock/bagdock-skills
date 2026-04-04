# Bagdock Skills

A collection of skills for AI coding agents following the [Agent Skills](https://github.com/anthropics/agent-skills) format. Available as a plugin for Claude Code, Cursor, OpenAI Codex, and Conductor. Includes an MCP server for tool access.

## Install

```bash
npx skills add bagdock/bagdock-skills
```

Then select the ones you wish to install.

## Available Skills

| Skill | Description | Source |
|-------|-------------|--------|
| [bagdock](skills/bagdock) | Bagdock platform API — apps, edges, auth, marketplace | Authored here |
| [bagdock-cli](skills/bagdock-cli) | Operate Bagdock from the terminal | Synced from [bagdock/bagdock-cli](https://github.com/bagdock/bagdock-cli) |

## MCP Server

The plugin includes the Bagdock MCP server, giving agents tool access to the full Bagdock API.

```json
{
  "mcpServers": {
    "bagdock": {
      "command": "npx",
      "args": ["-y", "bagdock-mcp"],
      "env": {
        "BAGDOCK_API_KEY": "your_api_key"
      }
    }
  }
}
```

## Plugins

This repo serves as a plugin for multiple platforms:

- **Cursor** — `.cursor-plugin/`
- **Claude Code** — `.claude-plugin/`
- **OpenAI Codex** — `.codex-plugin/`
- **Conductor** — Uses `claude mcp add` (see AGENTS.md)

## Editing skills

Skills marked **"Authored here"** can be edited directly in this repo.

Skills marked **"Synced from"** are automatically synced from their source repos. **Do not edit them here** — changes will be overwritten on the next sync. Edit in the source repo instead.

## Prerequisites

- A Bagdock account with a developer or operator role
- API key stored in `BAGDOCK_API_KEY` environment variable

Get your API key at [app.bagdock.com/settings/api-keys](https://app.bagdock.com/settings/api-keys)

## License

MIT
