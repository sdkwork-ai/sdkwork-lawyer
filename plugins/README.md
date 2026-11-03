# plugins/

- Purpose: application/runtime plugin **source** — marketplace plugin implementations and extension
  packages that ship with or install into SDKWork Lawyer.
- Owner: SDKWork maintainers.
- Status: inactive — no runtime plugin is authored yet.

## Allowed Content

- `<plugin-name>/README.md`, `specs/component.spec.json`, `src/`, and `tests/` for each runtime plugin.
- Plugin manifests and capability declarations consumed by the application runtime.

## Forbidden Content

- Agent plugin workspaces for coding tools — those live in `.sdkwork/plugins/` and declare
  `.codex-plugin/plugin.json`.
- Generated SDK output, build artifacts, or vendored external toolchains.
- Secrets, tokens, private certificates, or user-private configuration.
- Business authorization and domain services that belong in application packages or crates.

## Related Specs

- `COMPONENT_SPEC.md` — component contract for an authored package or plugin.
- `MODULE_SPEC.md` — appbase module shape when the plugin owns module behavior.
- `DEPENDENCY_MANAGEMENT_SPEC.md` — dependency and vendoring rules.

## Verification

```bash
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
node ../sdkwork-specs/tools/check-component-port-bindings.mjs --root .
```

Checklist: every plugin has a component spec; no agent-only plugin content; no vendored dependency
tree committed as authored source.
