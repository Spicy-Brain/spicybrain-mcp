# SpicyBrain MCP

[SpicyBrain](https://spicybrain.help) is an ADHD-friendly app for running your life and home. It is built around reminders that repeat at the right local time, tasks with subtasks, projects with board columns, and a Today list for what you're focusing on.

This repo is how you connect SpicyBrain to AI assistants. It holds:

- a plugin for **Claude Code** and **Codex** that adds the SpicyBrain server plus a skill that teaches the model to use it well
- `server.json`, the listing for the official [MCP Registry](https://registry.modelcontextprotocol.io)

The server itself runs at:

```text
https://spicybrain.help/mcp
```

It uses streamable HTTP and OAuth. You sign in with your SpicyBrain account. There are no API keys or headers to set.

## Install

Pick the app you use. Step-by-step guides with screenshots are at [spicybrain.help/connect](https://spicybrain.help/connect).

### Claude (web, desktop and mobile)

1. Open **Customize → Connectors**.
2. Choose **Add custom connector**.
3. Paste `https://spicybrain.help/mcp` and sign in to SpicyBrain when asked.

The Free plan allows one custom connector. On Team and Enterprise plans, an Owner adds it in **Organization settings → Connectors**, then members connect their own accounts.

SpicyBrain will also appear in the Claude Connectors Directory once it is listed there.

### ChatGPT

SpicyBrain for ChatGPT is on its way. It will be available from the ChatGPT apps directory once it is listed.

### Claude Code

Add the server:

```bash
claude mcp add --transport http spicybrain https://spicybrain.help/mcp
```

Then run `/mcp` in Claude Code, pick `spicybrain` and sign in.

Or install the plugin, which adds the same server plus the SpicyBrain skill:

```text
/plugin marketplace add Spicy-Brain/spicybrain-mcp
/plugin install spicybrain@spicybrain
```

Then run `/mcp` to sign in. Use one method, not both.

### Codex

Add the server:

```bash
codex mcp add spicybrain --url https://spicybrain.help/mcp
```

Codex opens your browser to sign in. If it doesn't, run `codex mcp login spicybrain`.

Or install the plugin, which adds the same server plus the SpicyBrain skill:

```bash
codex plugin marketplace add Spicy-Brain/spicybrain-mcp
codex plugin add spicybrain@spicybrain
```

You can also add the marketplace and then install SpicyBrain from `/plugins` inside Codex. Codex asks you to sign in the first time you use it. Use one method, not both.

### Cursor, VS Code and other MCP clients

Any client that supports remote MCP servers with OAuth can connect to `https://spicybrain.help/mcp`. See [spicybrain.help/connect](https://spicybrain.help/connect) for client-specific steps.

## What you can do

- Reminders: list, search, create, edit one occurrence or the whole series, complete, move to tomorrow, stop a series, delete
- Tasks: list, search, create, edit, add subtasks, reorder, complete, reopen, delete, restore
- Projects and board stages: create, rename, reorder, move tasks between columns
- Today list: add or remove tasks

The assistant asks before anything destructive, such as completing a task with subtasks, stopping a repeating reminder or deleting something.

## Disconnecting

Remove SpicyBrain in the app you connected it to. To revoke access from SpicyBrain's side, go to **Settings → Connected apps** on [spicybrain.help](https://spicybrain.help).

## Privacy and security

- This repo contains no credentials. Sign-in happens between your client and spicybrain.help using OAuth.
- The assistant only sees what your SpicyBrain account can see.
- Read the [privacy policy](https://spicybrain.help/privacy) and [terms](https://spicybrain.help/terms).

## Support

- Help: [spicybrain.help/support](https://spicybrain.help/support)
- Email: [admin@spicybrain.help](mailto:admin@spicybrain.help)
- Problems with this plugin: [open an issue](https://github.com/Spicy-Brain/spicybrain-mcp/issues)

## Development

Load the plugin from a checkout:

```bash
claude --plugin-dir ./plugins/spicybrain
```

Validate the Claude Code manifests:

```bash
claude plugin validate . --strict
claude plugin validate ./plugins/spicybrain --strict
```

To test against another deployment, add it as a separate server instead of editing the plugin:

```bash
claude mcp add --transport http spicybrain-dev https://your-host.example/mcp
```

See [RELEASING.md](RELEASING.md) for versioning and publishing.

## License

[MIT](LICENSE)
