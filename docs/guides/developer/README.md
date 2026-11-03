# Developer Guide

Status: draft — repository initialized, no language toolchain yet
Owner: SDKWork maintainers
Specs: DOCUMENTATION_SPEC.md, CODE_STYLE_SPEC.md, TEST_SPEC.md, PNPM_SCRIPT_SPEC.md

## Current State

`SDKWork Lawyer` carries the SDKWork repository contract only: baseline entrypoints, Canon
documentation, `.sdkwork/` workspace, and the standard root directory dictionary. There is no
application surface, API contract, SDK family, database module, or build pipeline yet, so there is
nothing to install, build, or run.

Read [../../AGENTS.md](../../AGENTS.md) before changing anything; it holds the execution rules and
the task-to-spec routing table.

## Working In This Repository

1. Read the nearest `AGENTS.md`, then only the specs the task names.
2. Decide where the change belongs using the root directory dictionary in
   [../../README.md](../../README.md). Do not invent a competing top-level directory.
3. Author the contract before the implementation: a requirement record, an ADR, or the API/SDK
   authority that the code must satisfy.
4. Run the narrowest verification for the changed surface.

## Verification

Repository-contract checks, run from the repository root:

```bash
node ../sdkwork-specs/tools/audit-repository-baseline.mjs --root .
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
node ../sdkwork-specs/tools/check-workspace-packages-layout.mjs --root . --mode enforce
node ../sdkwork-specs/tools/check-repository-docs-standard.mjs --root .
node ../sdkwork-specs/tools/check-apps-directory-index.mjs --root .
node ../sdkwork-specs/tools/check-gitignore-standard.mjs --root .
```

`check-agent-workflow-standard.mjs --root .` additionally requires release entrypoints
(`agent.workflow.json`, `.github/workflows/package.yml`) that land with the first application
surface. Do not create them ahead of the surface.

## First Surface Checklist

When the first application root is authorized:

- [ ] Record the architecture decision in `docs/architecture/decisions/`.
- [ ] Create `apps/sdkwork-lawyer-<client-arch>/` with `README.md`, `AGENTS.md`, `.sdkwork/`, and
      `agent.app.config.json`.
- [ ] Add the root to `apps/README.md`, to the root workspace manifests, and to
      `agent.workflow.json`.
- [ ] Add `package.json` scripts per `PNPM_SCRIPT_SPEC.md` and the thin
      `.github/workflows/package.yml` / `verify.yml` callers per `GITHUB_WORKFLOW_SPEC.md`.
- [ ] Author `etc/` profiles for each supported runtime target (`SOURCE_CONFIG_SPEC.md`).

## Related

- [../../README.md](../../README.md) — root layout and active capabilities.
- [../product/prd/PRD.md](../product/prd/PRD.md) — product Canon (draft).
- [../architecture/tech/TECH_ARCHITECTURE.md](../architecture/tech/TECH_ARCHITECTURE.md) — architecture Canon (draft).
