# Changelog

## 1.0.0 - 2026-09-29

First public release.

- Plugin for Claude Code and Codex that connects to the SpicyBrain MCP server at `https://spicybrain.help/mcp`.
- SpicyBrain skill covering reminders, tasks, subtasks, projects, board stages and the Today list, with confirmation before destructive actions.
- Claude Code marketplace (`.claude-plugin/marketplace.json`) and Codex marketplace (`.agents/plugins/marketplace.json`).
- `server.json` for the official MCP Registry as `io.github.Spicy-Brain/spicybrain`.
- Workflow that publishes `server.json` to the MCP Registry when a `v*` tag is pushed.
