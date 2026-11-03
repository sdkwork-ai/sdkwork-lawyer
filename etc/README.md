# etc/

- Purpose: source-controlled, secret-free deployment and runtime **profiles** and templates for the
  independently deployable roots of this repository.
- Owner: SDKWork maintainers; each deployable root owns its own `etc/` profiles.
- Status: inactive — no deployable root exists yet (`agent.app.config.json` is not authored), so no
  profile instance exists. This README records the contract for the first one.

## Allowed Content

- `sdkwork.deployment.config.json` — typed deployment index for a deployable root.
- Typed source configuration entrypoints and `standalone` / `cloud` ×
  `development` / `test` / `staging` / `demo` / `production` profile files.
- Environment templates copied from `../sdkwork-specs/templates/environment/`.
- Secret **references** (a pointer to a secret source), never secret values.

## Forbidden Content

- Live secrets, tokens, private keys, passwords, or real connection strings.
- User-private or environment-private runtime configuration. That lives under
  `~/.sdkwork/<application-code>` (or `%USERPROFILE%\.sdkwork\<application-code>`) per
  `RUNTIME_DIRECTORY_SPEC.md` and is never committed.
- The retired repository-root `configs/` layout, or a duplicate copy of a profile owned by another
  deployable root.
- Environment-specific values inside `agent.app.config.json` — the manifest declares identity,
  runtime targets, and references; `etc/` owns the values.

## Related Specs

- `SOURCE_CONFIG_SPEC.md` — `etc/` ownership, profile naming, and secret boundaries.
- `CONFIG_SPEC.md`, `ENVIRONMENT_SPEC.md` — configuration model and environment layering.
- `RUNTIME_DIRECTORY_SPEC.md` — user-private runtime paths.
- `DEPLOYMENT_SPEC.md` — how a profile maps to a deployment.
- `SECURITY_SPEC.md` — secret handling and redaction.

## Verification

```bash
node ../sdkwork-specs/tools/check-source-config-standard.mjs --root .
node ../sdkwork-specs/tools/audit-env-standard-workspace.mjs --workspace ..
```

Checklist: `agent.app.config.json` contains no concrete environment values; every profile is
secret-free, typed, and references only files inside `etc/`; no `configs/` directory exists.
