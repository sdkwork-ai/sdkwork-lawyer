# tests/

- Purpose: cross-package, contract, integration, end-to-end, fixture, and static verification that
  spans more than one package, crate, or module.
- Owner: SDKWork maintainers.
- Status: inactive — no test suite exists yet.

## Allowed Content

- `contract/` — API, SDK, and schema contract tests.
- `integration/` — cross-package and cross-service integration tests.
- `e2e/` — end-to-end flows against a runnable composition.
- `fixtures/` — safe, synthetic fixtures.
- `static/` — repository-level static verification inputs.

## Forbidden Content

- Package-local unit tests — those stay beside the package, crate, or module they verify.
- Real secrets, tokens, private certificates, customer data, or production dumps in fixtures.
- Runtime databases or captured state committed as test data.
- A test that silently skips instead of failing when its required contract is missing.

## Related Specs

- `TEST_SPEC.md` — contract, module, security, and parity test requirements.
- `QUALITY_GATE_SPEC.md` — ready/merge/release gates.
- `CODE_REVIEW_SPEC.md` — review expectations for test coverage.
- `SECURITY_SPEC.md`, `PRIVACY_SPEC.md` — safe test data.

## Verification

```bash
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
```

Checklist: fixtures contain no real secrets or customer data; each suite states the contract it
protects; package-local unit tests are not centralized here.
