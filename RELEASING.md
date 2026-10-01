# Releasing

## 1. Bump the version

Use the same version everywhere:

- `plugins/spicybrain/.claude-plugin/plugin.json` → `version`
- `plugins/spicybrain/.codex-plugin/plugin.json` → `version`
- `server.json` → `version`

Add an entry to `CHANGELOG.md`.

Claude Code only updates installed copies when the plugin version changes, so bump it for any change users should get, including skill edits. Don't add `version` to the marketplace entries; `plugin.json` is the single source.

## 2. Check

```bash
claude plugin validate . --strict
claude plugin validate ./plugins/spicybrain --strict
mcp-publisher validate
```

## 3. Tag

Merge to `main`, then:

```bash
git tag vX.Y.Z
git push origin vX.Y.Z
```

## 4. Publish server.json

Pushing a `v*` tag runs `.github/workflows/publish-mcp-registry.yml`. It checks that the tag matches `server.json`, signs in with GitHub OIDC and runs `mcp-publisher publish`. No secrets are needed.

To publish by hand instead, you must be an Owner of the `Spicy-Brain` GitHub organisation:

```bash
brew install mcp-publisher
mcp-publisher login github
mcp-publisher publish
```

The server name `io.github.Spicy-Brain/spicybrain` is case-sensitive and must match the organisation login exactly.

Plugin users get updates from the marketplaces; nothing else needs publishing.
