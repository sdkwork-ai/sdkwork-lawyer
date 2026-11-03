# tools/

- Purpose: repository-local reusable tooling that is not shipped as application runtime code —
  validators, generators, migration helpers, parsers, CLIs, and operator utilities.
- Owner: SDKWork maintainers.
- Status: inactive — no tool is authored yet; standards checks currently call `sdkwork-specs` tools.

## Allowed Content

- `validators/` — repository-specific static checks.
- `generators/` — code or artifact generators that are not the canonical SDK generator.
- `migrations/` — one-shot data or layout migration helpers.
- `operators/` — operator utilities for local or deployed environments.

## Forbidden Content

- Business logic that belongs in application source.
- Thin command wrappers that belong in `scripts/` — entrypoints stay there and call into `tools/`.
- A second SDK generator or a hand-rolled replacement for `@sdkwork/sdk-generator`.
- Credentials, private keys, or machine-specific absolute paths.
- Logic copied from `sdkwork-specs` instead of calling the canonical tool.

## Related Specs

- `CODE_STYLE_SPEC.md` — script style, build source integrity, deletion safety.
- `TYPESCRIPT_CODE_SPEC.md` §5 — Node script resilience.
- `MODULE_BIN_SPEC.md` — when a tool is exposed as a module `bin/` entrypoint.
- `TEST_SPEC.md` — tests required for authored tools.

## Verification

```bash
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
```

Checklist: every tool has a documented entrypoint and a test or narrow self-check; tools never
mutate version-control state; deletion inside a tool is explicit-path only.
