# crates/

- Purpose: Rust source — route crates, service crates, SQLx repository crates, hosts, workers, and
  reusable libraries for the SDKWork Lawyer application line.
- Owner: SDKWork maintainers; each crate is owned by the team that ships it.
- Status: inactive — no Rust source or `Cargo.toml` is authored yet.

## Allowed Content

- `sdkwork-routes-<capability>-<surface>/` — HTTP route crates.
- `sdkwork-<domain>-<capability>-service/` — domain service crates.
- `sdkwork-<domain>-<capability>-repository-sqlx/` — SQLx repository implementations.
- `sdkwork-<application-code>-service-host/`, `-native-host/`, `-tauri-host/` — hosts.
- `sdkwork-<domain>-<capability>-worker/` — background workers.
- `sdkwork-api-lawyer-assembly/`, `sdkwork-api-lawyer-standalone-gateway/` — API assembly and gateway.
- Reusable Rust libraries owned by this application line.

## Forbidden Content

- Business authorization, session, or app/domain service logic inside a native or Tauri host crate.
- Crate-local `migrations/` directories — database assets belong in root `database/` once it is
  activated (`DATABASE_FRAMEWORK_SPEC.md`).
- Hand-edited generated SDK output; generated clients under `sdks/`.
- Duplicated route definitions that bypass the authored contract in `apis/`.

## Related Specs

- `RUST_CODE_SPEC.md`, `NAMING_SPEC.md` §3.1/§3.2 — crate naming planes and dependency declaration.
- `APPLICATION_LAYERED_ARCHITECTURE_SPEC.md`, `APPLICATION_SPEC.md` — layering and crate roles.
- `API_SPEC.md`, `WEB_FRAMEWORK_SPEC.md`, `WEB_BACKEND_SPEC.md` — HTTP runtime contract.
- `DATABASE_SPEC.md`, `SUBJECT_ID_SPEC.md` — persistence and tenant/user scope.
- `TEST_SPEC.md` — required crate and contract tests.

## Verification

```bash
node ../sdkwork-specs/tools/check-rust-crate-naming-standard.mjs --root .
node ../sdkwork-specs/tools/check-rust-manifest-standard.mjs --root .
cargo test --workspace
```

Checklist: kebab-case package names with snake_case lib names; every external crate declared in the
owning manifest; `Cargo.lock` regenerated in the same change as a dependency edit.
