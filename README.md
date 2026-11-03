# SDKWork Lawyer

repository-kind: application

- Status: initialized — repository skeleton only; no runnable application surface yet
- Owner: SDKWork maintainers
- Application code: `lawyer`
- Standards entrypoint: [`../sdkwork-specs/README.md`](../sdkwork-specs/README.md)
- Layout authority: `SDKWORK_WORKSPACE_SPEC.md`

SDKWork Lawyer is the SDKWork application line for legal-practice work. This repository is
initialized against the SDKWork standards: the L1 repository baseline, the documentation Canon, the
`.sdkwork/` workspace, and the standard root directory dictionary exist and are verified by the
commands in [Verification](#verification).

Initialization deliberately stops at the repository contract. Product scope, application surface
architecture, API contracts, SDK families, database assets, application identity, and release
wiring are authored by later changes; they are not fabricated here. Each reserved directory that is
inactive is preserved as a tracked README that states the rules for filling it.

## Canon Documentation

| Document | Path |
| --- | --- |
| Documentation index | [docs/README.md](docs/README.md) |
| Product PRD | [docs/product/prd/PRD.md](docs/product/prd/PRD.md) |
| Technical architecture | [docs/architecture/tech/TECH_ARCHITECTURE.md](docs/architecture/tech/TECH_ARCHITECTURE.md) |

## Application Surfaces

[apps/README.md](apps/README.md) is the directory index for every application root below `apps/`.
No application root exists yet, so `apps/` currently declares the intended surface naming and the
rules a future surface must satisfy. The owner of this repository selects the first architecture
surface; until then no `apps/sdkwork-lawyer-*` root, `agent.app.config.json`, or architecture-specific
source tree is created.

## Active Root Layout

Every reserved directory below exists with a tracked `README.md`. Each directory README documents
purpose, owner, allowed content, forbidden content, related specs, and verification, as required by
`SDKWORK_WORKSPACE_SPEC.md` section 1.1.

```text
sdkwork-lawyer/
  AGENTS.md                 # agent execution entrypoint
  README.md                 # this file
  CLAUDE.md GEMINI.md CODEX.md   # tool compatibility shims to AGENTS.md
  .sdkwork/                 # source-controlled agent workspace metadata
  apis/                     # authored API contracts and API review inputs
  apps/                     # application root collection (index + future surfaces)
  crates/                   # Rust crates (route, service, repository, host, worker)
  sdks/                     # SDK family workspaces and generated SDK output
  jobs/                     # schedules, queue bindings, batch and maintenance definitions
  tools/                    # repository-local validators, generators, migration tools
  plugins/                  # application/runtime plugin source
  examples/                 # consumer-facing runnable and copyable examples
  etc/                      # source-controlled safe deployment/runtime profiles
  deployments/              # infrastructure descriptors, installers, rollout assets
  scripts/                  # thin command entrypoints
  docs/                     # Canon documentation, requirements, ADRs, guides, runbooks
  tests/                    # cross-package, contract, integration, e2e, static tests
```

`apis/` contains authored API contracts and API review inputs. `sdks/` is the SDK family and
generation workspace: it holds family manifests, materialized authority OpenAPI, derived `sdkgen`
inputs, and generator-owned output. The two directories are never conflated.

`plugins/` holds application/runtime plugin source. `.sdkwork/plugins/` holds repository/application
agent plugin workspaces for coding tools. They are different ownership domains and must not be
merged.

`etc/` holds source-controlled, secret-free deployment and runtime profiles and templates. User-private
or environment-private runtime configuration lives under `~/.sdkwork/<application-code>` and is
governed by `RUNTIME_DIRECTORY_SPEC.md`; it is never committed to `etc/`.

Intentionally absent until the matching capability is activated:

| Path | Activated when |
| --- | --- |
| `database/` | The application owns a database lifecycle contract, migrations, or seeds (`DATABASE_FRAMEWORK_SPEC.md`) |
| `specs/` | Repository-wide machine contracts exist; module-local specs live beside each module (`COMPONENT_SPEC.md`) |
| `assets/` | The first `agent.app.config.json` activates the governed asset root (`APP_ASSETS_SPEC.md`) |
| `agent.app.config.json`, `agent.workflow.json`, `agent.workflow.json` release targets | The first application surface and its release contract are authored (`APP_MANIFEST_SPEC.md`, `GITHUB_WORKFLOW_SPEC.md`) |
| `package.json`, `pnpm-workspace.yaml`, `Cargo.toml` | The first language toolchain is adopted (`PNPM_SCRIPT_SPEC.md`, `DEPENDENCY_MANAGEMENT_SPEC.md`) |

Repository-root `packages/`, `config/`, `generated/`, `services/`, `api/`, `sdk/`, `deploy/`, and
`tooling/` are not standard project-root names and must not be introduced; package families belong
under an application root as `apps/sdkwork-lawyer-<client-arch>/packages/`.

## Entry Points

- [AGENTS.md](AGENTS.md) — agent execution rules and standards routing.
- [.sdkwork/README.md](.sdkwork/README.md) — source-controlled agent workspace metadata.
- [docs/README.md](docs/README.md) — documentation routing by audience.
- [apps/README.md](apps/README.md) — application root index.

## Verification

Run the standards checks from this repository root:

```bash
node ../sdkwork-specs/tools/audit-repository-baseline.mjs --root .
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
node ../sdkwork-specs/tools/check-workspace-packages-layout.mjs --root . --mode enforce
node ../sdkwork-specs/tools/check-repository-docs-standard.mjs --root .
node ../sdkwork-specs/tools/check-apps-directory-index.mjs --root .
node ../sdkwork-specs/tools/check-gitignore-standard.mjs --root .
```

`check-agent-workflow-standard.mjs` validates the `AGENTS.md` entrypoints today and additionally
requires `agent.workflow.json` plus `.github/workflows/package.yml` only because this root declares
`repository-kind: application`. Those release entrypoints are not authored yet: packaging a
repository with no application surface would publish nothing, so the wiring lands together with the
first surface and its `agent.app.config.json` (`APP_MANIFEST_SPEC.md`, `GITHUB_WORKFLOW_SPEC.md`).

## Related Specs

- `SDKWORK_WORKSPACE_SPEC.md` — root directory dictionary and `.sdkwork/` contract.
- `REPOSITORY_BASELINE_SPEC.md` — L1 baseline files and `main`-branch development.
- `DOCUMENTATION_SPEC.md` — Canon documentation layout.
- `AGENTS_SPEC.md` — `AGENTS.md` sections, shims, and managed blocks.
- `APPLICATION_SPEC.md` — application root architecture and identity.
