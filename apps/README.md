# apps/

Application: lawyer
Status: initialized — no application root exists yet
Owner: SDKWork maintainers
Specs: APPLICATION_SPEC.md, SDKWORK_WORKSPACE_SPEC.md

This directory is the collection of independently runnable application roots for the SDKWork Lawyer
repository. Each direct child must be named `sdkwork-lawyer-<client-arch>/` and must be a complete
application root with its own `README.md`, `AGENTS.md`, `.sdkwork/`, and `agent.app.config.json`.

## Primary App Surface

The repository root is **not** currently the primary runnable app surface, and no child root is
either: initialization stops at the repository contract. The first application surface is selected
and authored by the repository owner, following exactly one root architecture standard:

| Surface role | Standard |
| --- | --- |
| `pc` | `APP_PC_ARCHITECTURE_SPEC.md` |
| `pad` | `APP_PAD_ARCHITECTURE_SPEC.md` |
| `h5` | `APP_H5_ARCHITECTURE_SPEC.md` |
| `flutter-mobile` | `FLUTTER_APP_MOBILE_ARCHITECTURE_SPEC.md` |
| `android-mobile` | `ANDROID_APP_MOBILE_ARCHITECTURE_SPEC.md` |
| `ios-mobile` | `IOS_APP_MOBILE_ARCHITECTURE_SPEC.md` |
| `harmony-mobile` | `HARMONY_APP_MOBILE_ARCHITECTURE_SPEC.md` |
| `mini-program` | `MINI_PROGRAM_APP_ARCHITECTURE_SPEC.md` |
| `uniapp` | `UNIAPP_APP_ARCHITECTURE_SPEC.md` |
| `unity` | `UNITY_APP_ARCHITECTURE_SPEC.md` |
| `static-web` | `APP_STATIC_WEB_ARCHITECTURE_SPEC.md` |
| `common` | shared package family, not runnable |

A cross-architecture TypeScript contract, service port, or RPC proto package lives under
`apps/sdkwork-lawyer-common/packages/`; client UI and host packages live under
`apps/sdkwork-lawyer-<client-arch>/packages/`. Repository-root `packages/` is forbidden.

## Directory Index

| Directory | Surface role | Runnable | Purpose | Entry |
| --- | --- | --- | --- | --- |
| — | — | — | No direct child directory exists yet | — |

`apps/` currently has **no child directories**. When the first application root is added, this table
must list it with its surface role, runnable flag, one-line purpose, and a relative link to the child
`README.md`. Stale entries must not remain after a child root is removed or renamed.

## Adding An Application Root

1. Read the matching root architecture standard and `APP_CLIENT_ARCHITECTURE_ALIGNMENT_SPEC.md`.
2. Create `apps/sdkwork-lawyer-<client-arch>/` with `README.md`, `AGENTS.md`, `.sdkwork/`,
   `agent.app.config.json`, and the architecture-mandated source, package, and config layout.
3. Update this index and the root `README.md` layout record.
4. Add the root to the parent workspace declarations (`pnpm-workspace.yaml` / `Cargo.toml`) exactly
   once, and register it in `agent.workflow.json` per `GITHUB_WORKFLOW_SPEC.md`.

## Verification

```bash
node ../sdkwork-specs/tools/check-apps-directory-index.mjs --root .
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
node ../sdkwork-specs/tools/check-client-host-packages.mjs --root .
```
