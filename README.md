# SpicyBrain for Claude

The official Claude plugin for [SpicyBrain](https://github.com/Spicy-Brain/SpicyBrain). It connects Claude to the hosted SpicyBrain MCP server and teaches Claude how to manage projects, tasks, and reminders safely.

## Install

In Claude Code, add the marketplace and install the plugin:

```text
/plugin marketplace add Spicy-Brain/SpicyBrainClaudeMcp
/plugin install spicybrain@spicybrain
```

Run `/reload-plugins` if Claude asks you to reload, then open `/mcp` and authenticate the `spicybrain` server with your SpicyBrain account.

The plugin is also suitable for Claude Cowork installations that support Claude plugins.

## Included capabilities

- Connect to the hosted SpicyBrain MCP server over HTTPS.
- List and create projects.
- List, search, create, and complete tasks.
- List, search, create, and complete reminders.
- Guide Claude through project resolution, recurrence, timezones, and safe mutations.

## Development

Load the plugin directly from a local checkout:

```bash
claude --plugin-dir ./plugins/spicybrain
```

Validate the marketplace and plugin before publishing:

```bash
claude plugin validate . --strict
claude plugin validate ./plugins/spicybrain --strict
```

The bundled server URL defaults to the current hosted beta endpoint. To test another deployment without editing the plugin, set `SPICYBRAIN_MCP_URL` to the full MCP endpoint before starting Claude Code:

```bash
export SPICYBRAIN_MCP_URL=https://example.com/mcp/spicybrain
```

## Security

The plugin contains no credentials. Authentication is handled by the SpicyBrain server through OAuth. Review tool calls before allowing mutations, and install plugins only from repositories you trust.

## License

MIT
