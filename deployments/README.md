# deployments/

- Purpose: infrastructure descriptors and release handoff material — container, cluster, service
  manager, proxy, installer, rollout, and rollback assets, plus deployment documentation.
- Owner: SDKWork maintainers.
- Status: inactive — nothing is deployed yet.

## Allowed Content

- `docker/`, `k8s/`, `systemd/`, `nginx/` (or `webserver/`) descriptor trees.
- Packaging handoff files and installer assets.
- `runbooks/` deployment procedures.
- Release artifact references and rollout/rollback plans.

## Forbidden Content

- Runtime value authority — concrete environment, Base URL, bind, and topology values belong in
  `etc/` profiles; descriptors reference them.
- Live secrets or private keys; secrets are injected by the environment, not committed.
- A second copy of application source or generated SDK output.
- Hand-maintained nginx site files where `sdkwork-webserver` configuration is the authority.

## Related Specs

- `DEPLOYMENT_SPEC.md`, `SDKWORK_DEPLOY_SPEC.md` — deployment model and typed deploy manifest.
- `PACKAGING_SPEC.md` — release artifact layout.
- `SDKWORK_WEBSERVER_SPEC.md`, `NGINX_SPEC.md` — proxy and static resource configuration.
- `OPERATIONS_SPEC.md`, `HEALTH_CHECK_SPEC.md` — operations lifecycle and readiness.
- `GITHUB_WORKFLOW_SPEC.md` — how deployment is triggered from CI.

## Verification

```bash
node ../sdkwork-specs/tools/check-webserver-toml-standard.mjs --root .
node ../sdkwork-specs/tools/check-deploy-standard.mjs --root .
```

Checklist: descriptors contain no secrets and no duplicated runtime values; every deployment
procedure has a rollback counterpart; generated proxy configuration matches the declared authority.
