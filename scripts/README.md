# scripts/

- Purpose: thin command entrypoints for build, verification, generation, migration, packaging, and
  release workflows.
- Owner: SDKWork maintainers.
- Status: inactive — no language toolchain or root script set exists yet.

## Allowed Content

- Thin shell, PowerShell, Node, or Python wrappers that resolve a root command and delegate.
- Application-internal runner file names that are implementation details of a documented command.

## Forbidden Content

- Reusable logic, parsers, generators, validators, or CLIs — those belong in `tools/` or a package.
- A second implementation of a canonical command (`pnpm build`, `pnpm verify`, `sdkgen`, …).
- Wildcard or recursive deletion; deletion must enumerate exact paths (`DESTRUCTIVE_OPERATION_SPEC.md`).
- Network, build, install, or publish steps combined with a deletion in one invocation.
- Secrets, tokens, or machine-specific absolute paths.

## Related Specs

- `PNPM_SCRIPT_SPEC.md` — public script names, lifecycle commands, and `clean` boundary.
- `CODE_STYLE_SPEC.md` §7/§8 — build source integrity and deletion safety.
- `MODULE_BIN_SPEC.md` — when a script is exposed as a module `bin/` entrypoint.
- `PORTABILITY_SPEC.md` — portability of shell and PowerShell entrypoints.

## Verification

```bash
node ../sdkwork-specs/tools/check-pnpm-script-standard.mjs --root .
node ../sdkwork-specs/tools/check-destructive-operation-patterns.mjs --workspace ..
```

Checklist: every script is a thin entrypoint; public `package.json` command names follow
`PNPM_SCRIPT_SPEC.md`; no wildcard deletion appears in any script.
