# Repository Agent Plugins

- Purpose: repository-local agent extensions packaged for SDKWork coding tools.
- Owner: SDKWork maintainers.
- Authority: `SDKWORK_WORKSPACE_SPEC.md` section 4 and `AGENTS_SPEC.md`.

## Plugin Layout

`<plugin-name>` uses lowercase kebab-case:

```text
.sdkwork/plugins/<plugin-name>/
  .codex-plugin/
    plugin.json       # required for an installable plugin
  skills/             # optional
  mcp/                # optional: MCP server definitions
  apps/               # optional
  scripts/            # optional
```

`plugin.json` identifies the plugin name, version, owner, description, and contributed
skills/tools/apps when the plugin framework supports those fields.

## Rules

- Plugin skills follow the same rules as `.sdkwork/skills/`.
- Plugins may contain MCP server definitions, app definitions, scripts, or bundled assets only when
  they are repository-specific and documented.
- Plugins must not vendor unrelated external toolchains, generated SDK output, secrets, runtime
  databases, caches, logs, or user-private data.
- A plugin that wraps build, SDK generation, or deployment commands calls the canonical command
  defined by the relevant spec; it must never substitute a local stub or incompatible generator.
- Application/runtime plugin **source** belongs in root `plugins/`, not here. This directory holds
  agent plugin workspaces only.

## Verification

```bash
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
```

Checklist: every installable plugin has `.codex-plugin/plugin.json`; no plugin bundles secrets or
generated output.
