# jobs/

- Purpose: non-request/response work — schedules, queue bindings, batch descriptors, maintenance
  tasks, and their runbooks.
- Owner: SDKWork maintainers.
- Status: inactive — no job is defined yet.

## Allowed Content

- `schedules/` — cron and scheduled task declarations.
- `queues/` — queue consumer bindings and retry/dead-letter policy references.
- `batches/` — batch job descriptors.
- `runbooks/` — maintenance procedures generated or authored per `OPERATIONS_SPEC.md`.
- `packages/` — non-Rust job packages when a job cannot be a Rust worker.

## Forbidden Content

- Rust worker implementations — those live in `crates/sdkwork-<domain>-<capability>-worker/`.
- Request/response API handlers.
- Secrets, live connection strings, or environment-private values; jobs read configuration from
  `etc/` profiles or the runtime configuration provider.
- Duplicate schedule definitions spread across CI files and `docs/`.

## Related Specs

- `EVENT_SPEC.md` — async APIs, domain events, outbox, webhooks.
- `OPERATIONS_SPEC.md` — schedules, runbooks, backup/restore and alerting lifecycle.
- `OBSERVABILITY_SPEC.md` — logs, metrics, traces for background work.
- `DEPLOYMENT_SPEC.md` — how a scheduled workload is deployed.

## Verification

```bash
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
```

Checklist: every schedule is declared once and references an owned worker or package; every runbook
carries its generator marker when generated; no worker implementation is duplicated here.
