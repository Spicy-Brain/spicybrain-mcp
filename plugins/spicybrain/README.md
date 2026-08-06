# SpicyBrain plugin

This plugin connects Claude to the hosted SpicyBrain MCP server and provides workflow guidance for projects, tasks, and reminders.

## Authentication

After installation, use `/mcp` in Claude Code, select `spicybrain`, and complete the SpicyBrain OAuth flow. The plugin does not store credentials.

## Configuration

The MCP endpoint can be overridden for development by setting `SPICYBRAIN_MCP_URL` to the complete endpoint URL before starting Claude Code.

## Manual skill invocation

Claude can activate the skill automatically when a request relates to SpicyBrain. It can also be invoked directly:

```text
/spicybrain:spicybrain
```
