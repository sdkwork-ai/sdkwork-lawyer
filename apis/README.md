# apis/

- Purpose: authored API contracts and API review inputs for the SDKWork Lawyer application line —
  OpenAPI authorities, RPC/proto contracts, async/event manifests, examples, changelogs, and
  validation fixtures.
- Owner: SDKWork maintainers; each API surface is owned by the team that publishes it.
- Status: inactive — no API contract is authored yet. The directory exists so that the first
  contract lands at its canonical path instead of an ad-hoc `api/` or `specs/` location.

## Allowed Content

- `open-api/<domain>/openapi.yaml` — SDKWork-owned business open API and vendor compatibility surfaces.
- `app-api/<domain>/openapi.yaml` — application-facing API.
- `backend-api/<domain>/openapi.yaml` — backend/admin API.
- `rpc/` — proto packages and RPC contract sources.
- `async/` — AsyncAPI or event manifests.
- `internal/` — internal service contracts that are not public surfaces.
- Per-surface `routes/`, `schemas/`, `examples/`, `changelogs/`, `tests/` support material.

## Forbidden Content

- Generated SDK transport packages, SDK family directories, or generator-owned
  `.sdkwork/sdkwork-generator-*.json` files — those belong under `sdks/`.
- Server, handler, repository, or client implementation code.
- Live secrets, tokens, private keys, or customer data in examples and fixtures.
- Hand-written HTTP code that redefines the contract instead of being driven by it.

## Related Specs

- `API_SPEC.md` — envelope, operation patterns, error model, `int64` wire contract.
- `PAGINATION_SPEC.md` — list/search pagination contract; verify with `check-pagination.mjs`.
- `API_ASSEMBLY_SPEC.md`, `WEB_FRAMEWORK_SPEC.md`, `WEB_BACKEND_SPEC.md` — runtime and assembly.
- `SDK_SPEC.md`, `SDK_WORKSPACE_GENERATION_SPEC.md` — how contracts feed SDK generation.
- `TEST_SPEC.md` — required contract tests.

## Verification

```bash
node ../sdkwork-specs/tools/check-api-operation-patterns.mjs --workspace ..
node ../sdkwork-specs/tools/check-api-response-envelope.mjs --workspace ..
node ../sdkwork-specs/tools/check-pagination.mjs --workspace ..
```

Checklist: every authored operation declares its wire protocol, success envelope, and error model;
every `int64` field is a string on the wire; no generated SDK output lives here.
