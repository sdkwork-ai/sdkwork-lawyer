# .sdkwork/ Workspace

- Purpose: source-controlled agent development metadata for the SDKWork Lawyer repository.
- Owner: SDKWork maintainers.
- Authority: `SDKWORK_WORKSPACE_SPEC.md` (this directory), `AGENTS_SPEC.md`, and `SOUL.md`.

`.sdkwork/` is **not** runtime state. It stores repository-local skills, agent plugins, and optional
machine-readable workspace manifests so agents, developers, and CI share the same project knowledge.
User-private runtime configuration, databases, caches, logs, and secrets live under
`~/.sdkwork/<application-code>` (or `%USERPROFILE%\.sdkwork\<application-code>`) per
`RUNTIME_DIRECTORY_SPEC.md` and are never copied into this directory in committed form.

Execution order is owned by [../AGENTS.md](../AGENTS.md); shared agent behavior is owned by
`../sdkwork-specs/SOUL.md`. This README only describes what lives here.

## Contents

| Path | Authoritative for | Committed |
| --- | --- | --- |
| `skills/` | Repository-local agent skills; each real skill has `skills/<name>/SKILL.md` | Yes |
| `plugins/` | Repository-local agent plugin workspaces; installable plugins declare `.codex-plugin/plugin.json` | Yes |
| `manifests/` | Optional machine-readable workspace manifests (`kind: sdkwork.workspace`) | Yes, when present |
| `local/`, `tmp/`, `cache/`, `secrets/`, `manual-backups/` | Local-only scratch and private state | No — ignored by `.gitignore` |

## Rules

- Skills and plugins cite canonical `sdkwork-specs` instead of copying normative rule bodies.
- A script under this directory that contacts an external service documents the service, credential
  source, dry-run behavior, and verification command.
- No secrets, tokens, private certificates, generated SDK output, runtime databases, caches, logs, or
  user-private files are committed here.
- Manifests under `manifests/` never redeclare SDKWork source dependency paths; those stay in the
  native build-tool workspace roots (`pnpm-workspace.yaml`, root `Cargo.toml`, root `pubspec.yaml`).

## Verification

```bash
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
node ../sdkwork-specs/tools/audit-repository-baseline.mjs --root .
```

Checklist: every committed skill has `SKILL.md`; every installable plugin has
`.codex-plugin/plugin.json`; ignored state directories contain nothing committed.
