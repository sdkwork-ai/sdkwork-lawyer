# SDKWork Lawyer Technical Architecture

Status: draft
Owner: SDKWork maintainers
Updated: 2026-11-03
Specs: ARCHITECTURE_DECISION_SPEC.md, DOCUMENTATION_SPEC.md

## Document Map

- Add `TECH-<topic>.md` shards in this directory when the architecture grows beyond one reviewable screen.

## 1. Architecture Overview

No runtime architecture is decided yet. What exists is the repository contract fixed by
`SDKWORK_WORKSPACE_SPEC.md`: the root directory dictionary, the `.sdkwork/` workspace, the Canon
documentation entrypoints, and the agent entrypoints.

Runtime architecture will be recorded as architecture decision records under
`docs/architecture/decisions/` **before** the corresponding implementation is authored, per
`ARCHITECTURE_DECISION_SPEC.md`. The first three decisions required are:

1. Application surface architecture (PC, H5, pad, Flutter, mini program, …) and its host family.
2. Server runtime and API assembly shape, if the product serves HTTP APIs.
3. Data ownership: relational schema ownership, tenant/subject scope, and migration authority.

## 2. Technology Choices

Not decided. Candidate stacks must satisfy the SDKWork standards rather than the reverse:

- Server/API and hosts: Rust with the SDKWork web framework and route/service/repository layering
  (`APPLICATION_LAYERED_ARCHITECTURE_SPEC.md`, `RUST_CODE_SPEC.md`).
- Client surfaces: the selected architecture standard (React for PC/H5/pad, Flutter or native for
  mobile, and so on), with generated SDK clients instead of hand-written HTTP.
- Data: PostgreSQL authoritative-server layout once `database/` is activated
  (`DATABASE_SPEC.md`, `DATABASE_FRAMEWORK_SPEC.md`).

No dependency is adopted in this document; adoption is an ADR plus a manifest change.

## 3. System Boundaries And Modules

The reserved root boundaries are declared before any module exists:

| Boundary | Owner | Content |
| --- | --- | --- |
| `apis/` | API owners | Authored contracts only; no implementation |
| `apps/` | Surface owners | Runnable application roots and their architecture-local packages |
| `crates/` | Service owners | Rust route, service, repository, host, worker, library crates |
| `sdks/` | Generator (`sdkgen`) | Family manifests, authority OpenAPI, generated output |
| `database/` (later) | Data owner | Contract, migrations, seeds, drift policy |
| `etc/` | Deployable-root owner | Safe profiles and templates; no secrets |
| `deployments/` | Operations owner | Infrastructure descriptors and release handoff |
| `docs/` | All owners | Canon PRD, architecture, requirements, ADRs, guides, runbooks |

Modules appear only with their own `specs/component.spec.json` and `AGENTS.md` when the module is
independently built, distributed, or long-lived (`COMPONENT_SPEC.md`).

## 4. Directory And Package Layout

Authored source lives under an application root (`apps/sdkwork-lawyer-<client-arch>/`) or a crate,
never at the repository root. Package families live under
`apps/sdkwork-lawyer-common/packages/` (cross-architecture contracts, ports, RPC proto) or
`apps/sdkwork-lawyer-<client-arch>/packages/` (client UI and host packages).

Repository-root `packages/`, `config/`, `generated/`, `services/`, `api/`, `sdk/`, `deploy/`, and
`tooling/` do not exist and must not be introduced. Package boundaries are declared in
`pnpm-workspace.yaml` / `Cargo.toml` at the consuming root exactly once.

## 5. API, SDK, And Data Ownership

- `apis/` owns the authored contract: OpenAPI authorities, proto packages, async manifests.
- `sdks/` projects that contract into generated clients; generated output is never hand-edited.
- A generated `@sdkwork/*-app-sdk` / `@sdkwork/*-backend-sdk` client is the only client HTTP surface;
  raw HTTP is forbidden (`APP_SDK_INTEGRATION_SPEC.md`).
- The database contract, migrations, and seeds belong to root `database/` once activated; crate-local
  migrations are legacy.

## 6. Security, Privacy, And Observability

Legal-practice data is sensitive by nature. Before any feature stores or transmits matter, document,
or client data, the design must state:

- the data classes and their retention, residency, and deletion rules (`PRIVACY_SPEC.md`);
- authentication, authorization, and tenant/subject isolation (`IAM_SPEC.md`, `SUBJECT_ID_SPEC.md`,
  `SECURITY_SPEC.md`);
- audit, log, metric, and trace coverage including correlation ids (`OBSERVABILITY_SPEC.md`);
- secret handling: references only in `etc/`, values injected at runtime.

## 7. Deployment And Runtime Topology

Not decided. When a deployable root exists, `etc/` owns `standalone`/`cloud` × environment profiles,
`deployments/` owns the infrastructure descriptors, and `agent.app.config.json` declares supported
runtime targets. No environment value is committed outside `etc/`.

## 8. Architecture Decision Index

| ADR | Title | Status |
| --- | --- | --- |
| — | No architecture decision recorded yet | — |

New ADRs use `ADR-YYYYMMDD-<short-title>.md` in `docs/architecture/decisions/`.

## 9. Verification

```bash
node ../sdkwork-specs/tools/check-repository-docs-standard.mjs --root .
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
node ../sdkwork-specs/tools/check-apps-directory-index.mjs --root .
```

Architecture claims are verified by the gate named in the owning spec (application manifest,
package layout, source config, API contract, SDK generation), not by this document.
