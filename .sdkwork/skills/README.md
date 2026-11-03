# Repository Skills

- Purpose: reusable agent/operator workflows for the SDKWork Lawyer repository.
- Owner: SDKWork maintainers.
- Authority: `SDKWORK_WORKSPACE_SPEC.md` section 3 and `AGENTS_SPEC.md`.

## Adding A Skill

Create one directory per skill using lowercase kebab-case:

```text
.sdkwork/skills/<skill-name>/
  SKILL.md          # required entrypoint
  references/       # optional: cited standards or repository contracts
  scripts/          # optional: deterministic, documented scripts
  assets/           # optional: inputs the workflow needs
```

`SKILL.md` must state when to use the skill, the inputs it expects, the files or commands it may
touch, and which root specs it follows. Common skills cite canonical `sdkwork-specs` rather than
copying them — for example an SDK generation skill cites `SDK_SPEC.md` and
`SDK_WORKSPACE_GENERATION_SPEC.md`.

## Rules

- A skill must not weaken root specs, bypass SDK generation standards, replace generated SDK clients
  with raw HTTP, or redefine API, security, or runtime rules.
- Skills never store application/runtime source, generated SDK output, runtime data, secrets, API
  keys, auth tokens, private certificates, or user-private files.
- Not every capability belongs here: product behavior belongs in source, contracts belong in
  `specs/`, and operator procedures belong in `docs/runbooks/`. A skill is for repeated agent work.

## Recommended Categories

- API route and OpenAPI materialization.
- SDK generation and generated-client verification.
- Repository/component standards inventory.
- Release and deployment readiness checks.

## Verification

```bash
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
```

Checklist: every skill directory contains `SKILL.md`; no skill duplicates a normative spec body.
