# examples/

- Purpose: consumer-facing examples for this repository's APIs, SDKs, and configuration — runnable
  demos and copyable snippets.
- Owner: SDKWork maintainers.
- Status: inactive — no example is authored yet.

## Allowed Content

- Runnable integration examples that consume a generated SDK or a documented API.
- Sample `etc/` profile templates that are secret-free and reference-only.
- Copyable configuration snippets with an explicit explanation of required inputs.

## Forbidden Content

- Real credentials, tokens, private certificates, or customer data.
- A fork of application source kept only to demonstrate a feature.
- Examples that hand-roll HTTP where a generated SDK exists.
- Generated SDK output or build artifacts.

## Related Specs

- `SDK_SPEC.md`, `APP_SDK_INTEGRATION_SPEC.md` — how an example consumes a generated client.
- `API_SPEC.md` — request/response examples and error shapes.
- `DOCUMENTATION_SPEC.md` — documentation expectations for published examples.

## Verification

```bash
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
```

Checklist: each example states its prerequisites and run command; no example embeds a secret; every
example still compiles and runs against the current contract.
