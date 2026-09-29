# SpicyBrain plugin

Connects Claude Code or Codex to the SpicyBrain MCP server at `https://spicybrain.help/mcp` and adds a skill that teaches the model how to use SpicyBrain's reminders, tasks, projects and Today list safely.

## What's inside

| Path | Purpose |
| --- | --- |
| `.mcp.json` | The remote MCP server, used by both Claude Code and Codex |
| `.claude-plugin/plugin.json` | Claude Code manifest |
| `.codex-plugin/plugin.json` | Codex manifest |
| `skills/spicybrain/SKILL.md` | Guidance for the model |
| `assets/logo.png` | Icon shown in Codex |

## Signing in

You sign in with your SpicyBrain account the first time a tool is used. The plugin holds no credentials.

- Claude Code: run `/mcp`, pick `spicybrain` and sign in.
- Codex: run `codex mcp login spicybrain` if Codex doesn't prompt you.

To use the skill directly in Claude Code, run `/spicybrain:spicybrain`.

See the [main README](../../README.md) for install steps.
