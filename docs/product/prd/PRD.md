# SDKWork Lawyer PRD

Status: draft
Owner: SDKWork maintainers
Application: lawyer
Updated: 2026-11-03
Specs: REQUIREMENTS_SPEC.md, DOCUMENTATION_SPEC.md

## Document Map

- Add `PRD-<topic>.md` shards in this directory when the PRD grows beyond one reviewable screen.

## 1. Background And Problem

SDKWork Lawyer is initialized as an application line for legal-practice work. The repository
currently carries the SDKWork repository contract — baseline entrypoints, the documentation Canon,
the `.sdkwork/` workspace, and the standard root directory dictionary — and no product behavior.

No product problem statement has been validated yet. This section stays a placeholder until
requirements discovery produces an approved `REQ-*` record under
[docs/product/requirements/](../requirements/) per `REQUIREMENTS_SPEC.md`. Do not treat the working
hypothesis below as committed scope.

## 2. Target Users

Not yet validated. Working hypothesis to confirm or discard during discovery:

- Legal practitioners who need to organize matters, documents, and deadlines.
- Law-firm operations staff who coordinate intake, assignments, and billing.
- Clients who need a scoped view of their own matter.

Each candidate segment must be evidenced by a requirement record before it drives design.

## 3. Goals And Non-Goals

Goals already achieved by initialization:

- The repository satisfies the SDKWork L1 baseline and layout standard.
- Canon documentation entrypoints exist and are linked from the root.
- Every reserved root directory states its ownership and boundary before content exists.

Product goals: not yet defined. They become `REQ-*` records with acceptance criteria.

Non-goals at this stage:

- No application surface, API contract, SDK family, database module, or release pipeline is claimed.
- No customer, matter, or document data is modeled before privacy and tenancy are decided.

## 4. Scope

In scope now: the repository contract and its verification.

Out of scope until a later approved change: user-facing features, data model, API surface, client
architecture, deployment topology, and release artefacts.

## 5. User Scenarios

None confirmed. Scenarios are written only after the target segment and the problem are validated,
and each one links to the requirement it justifies.

## 6. Success Metrics

Initialization metrics:

- Every standards check listed in the root `README.md` passes.
- The first approved `REQ-*` record exists before the first application surface is authored.

Product metrics (activation, retention, task completion, matter throughput) are defined with the
first validated requirement.

## 7. Phases

| Phase | Outcome | State |
| --- | --- | --- |
| 0. Repository initialization | Standards-compliant repository contract, Canon scaffolding, layout dictionary | Done |
| 1. Requirements discovery | Validated problem, target segment, and `REQ-*` records | Not started |
| 2. Architecture decision | ADRs for app surface, server runtime, data ownership, and tenancy | Not started |
| 3. First application surface | One runnable surface with an `agent.app.config.json` and release wiring | Not started |

## 8. Linked Requirements

None yet. Requirements use the `REQ-YYYY-MMDD-<slug>.md` naming convention in
`docs/product/requirements/`.

## 9. Open Questions

- Which client surfaces ship first — PC web, H5, pad, or a native mobile surface?
- Is the product single-tenant per deployment, or multi-tenant with per-firm isolation?
- Which legal-domain data classes are processed, and what retention, residency, and privilege
  constraints apply? (`PRIVACY_SPEC.md`, `SECURITY_SPEC.md`)
- Does the product integrate with existing document stores, calendars, or billing providers?
- What is the authentication and identity model — SDKWork IAM tenant app, or a federated directory?
