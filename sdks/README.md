# sdks/

- Purpose: the SDK family and generation workspace — family manifests, materialized authority
  OpenAPI, derived `sdkgen` inputs, generated language workspaces, and generated SDK output.
- Owner: `sdkgen` (`../sdkwork-sdk-generator`) owns generated output; SDKWork maintainers own the
  authored family manifests and generator inputs.
- Status: inactive — no SDK family is authored yet.

## Allowed Content

- SDK family manifests and `sdkwork-sdk.json` declarations.
- Materialized authority OpenAPI copied from `apis/` by the generator chain.
- Derived `*.sdkgen.*` generator inputs and route manifests.
- Generated language workspaces (`generated/server-openapi/…`) and the generator-owned
  `.sdkwork/sdkwork-generator-*.json` control-plane reports.
- Handwritten `custom/` roots and composed facades outside generated-owned trees.
- SDK component specs.

## Forbidden Content

- Hand-edited generated SDK source, type definitions, `dist/` bundles, or generated package metadata.
- Authored API contract sources that belong in `apis/`.
- Raw HTTP clients that replace a generated SDK client.
- Secrets, private certificates, or tokens in any SDK package.

## Generated Output Is Generator-Owned

`sdks/` generated trees are produced by the canonical generator
`../sdkwork-sdk-generator/bin/sdkgen.js` (`@sdkwork/sdk-generator`). When generated output does not
meet a contract, fix the upstream API authority, route manifest, generator profile, or `custom/`
build script, then regenerate. Never patch generated output in place, and never hand-prune a
generated tree — re-running the family generation command owns cleanup.

## Related Specs

- `SDK_SPEC.md`, `SDK_WORKSPACE_GENERATION_SPEC.md` — generation contract and package layout.
- `SDK_PACKAGE_NAMING_SPEC.md`, `SDK_MANIFEST_SPEC.md` — naming and manifest rules.
- `API_SPEC.md` — wire contract the SDKs project.
- `RPC_SDK_WORKSPACE_SPEC.md` — when RPC SDKs are generated.

## Verification

```bash
node ../sdkwork-specs/tools/sync-agent-sdk-generation-standard.mjs --root . --check
node ../sdkwork-specs/tools/check-sdk-standard.mjs --workspace ..
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
```

Checklist: no generated file carries a hand edit; regeneration reproduces the committed tree; every
family manifest declares its generation profile and authority source.
