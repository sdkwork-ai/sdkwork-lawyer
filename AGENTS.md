# Repository Guidelines

## SDKWORK Soul

Read [`../sdkwork-specs/SOUL.md`](../sdkwork-specs/SOUL.md) before executing tasks in this root.
Follow the governing spec before memory, the directory dictionary before broad context, stop on
ambiguity instead of inventing a contract, and report evidence before completion.

## SDKWORK Standards

Canonical SDKWork standards from this repository root:

- [`../sdkwork-specs/README.md`](../sdkwork-specs/README.md)
- [`../sdkwork-specs/SOUL.md`](../sdkwork-specs/SOUL.md)
- [`../sdkwork-specs/AGENTS_SPEC.md`](../sdkwork-specs/AGENTS_SPEC.md)

This repository follows those standards and does not copy their normative bodies locally. The
repository is expected to sit beside `sdkwork-specs/` in the standard multi-repository workspace; a
standalone checkout must locate the same paths from the workspace root. If a relative path does not
resolve, stop and report the broken workspace layout rather than substituting a guessed rule.

## Application Identity

Application code: `lawyer`. Product name: SDKWork Lawyer. This root currently has no
`agent.app.config.json` because the first application surface has not been authored. Once identity,
registration, runtime targets, client architectures, or release metadata are authored, that manifest
becomes the identity authority (`APP_MANIFEST_SPEC.md`).

`etc/` is the authority for concrete, secret-free environment, deployment-profile, Base URL, bind,
and topology values (`SOURCE_CONFIG_SPEC.md`). Do not move those values into the app manifest, into
source code, or into `docs/` prose, and do not commit user-private runtime configuration, which is
governed by `RUNTIME_DIRECTORY_SPEC.md`.

## Local Dictionary Structure

- `AGENTS.md` — this execution entrypoint.
- `README.md` — root layout documentation and the active/absent capability record.
- `CLAUDE.md`, `GEMINI.md`, `CODEX.md` — compatibility shims that point here; they carry no rule body.
- `.sdkwork/` — source-controlled agent workspace metadata: skills, plugins, optional manifests. It is not runtime state.
- `apis/` — authored API contracts and API review inputs (OpenAPI, proto, event manifests, examples).
- `apps/` — application roots; [apps/README.md](apps/README.md) is the directory index (`APPLICATION_SPEC.md`).
- `crates/` — Rust crates: route, service, repository, host, worker, reusable library.
- `sdks/` — SDK family workspaces, materialized authority OpenAPI, derived `sdkgen` inputs, and generator-owned output.
- `jobs/` — schedules, queue bindings, batch and maintenance job definitions and runbooks.
- `tools/` — repository-local validators, generators, migration tools, and operator utilities.
- `plugins/` — application/runtime plugin source; distinct from `.sdkwork/plugins/` agent plugin workspaces.
- `examples/` — consumer-facing runnable or copyable examples.
- `etc/` — source-controlled safe deployment/runtime profiles and templates (`SOURCE_CONFIG_SPEC.md`).
- `deployments/` — infrastructure descriptors, packaging handoff, installers, rollout and rollback assets.
- `scripts/` — thin command entrypoints only; reusable logic belongs in `tools/` or a package.
- `docs/` — Canon documentation, requirements, ADRs, plans, guides, runbooks. Entry points are
  [docs/README.md](docs/README.md), [docs/product/prd/PRD.md](docs/product/prd/PRD.md), and
  [docs/architecture/tech/TECH_ARCHITECTURE.md](docs/architecture/tech/TECH_ARCHITECTURE.md).
- `tests/` — cross-package, contract, integration, end-to-end, and static verification content.

Reserved directory names are fixed by `SDKWORK_WORKSPACE_SPEC.md` section 1.1. Do not introduce
competing root names such as `api/`, `sdk/`, `deploy/`, `deployment/`, `tooling/`, `config/`, or
repository-root `packages/`.

## Spec Resolution Order

Use dynamic progressive loading: resolve the nearest contract and the current task category first,
then read only the selected standard sections, then the implementation files. Do not preload the
whole standards catalog or every language spec.

1. This `AGENTS.md`.
2. `agent.app.config.json`, when it exists.
3. The nearest module `specs/README.md` and `specs/component.spec.json` when the task touches an authored module.
4. Root `specs/` when the task is repository-wide (`COMPONENT_SPEC.md`).
5. `.sdkwork/README.md` and only the skill or plugin whose trigger matches the task.
6. Global standards through `../sdkwork-specs/README.md`, then the task row's specs.
7. Implementation, test, and workflow files.

Local contracts may narrow a task, but global `sdkwork-specs` standards remain authoritative.

## Required Specs By Task Type

This table is a task gate, not a startup bundle.

| Task | Read before editing |
| --- | --- |
| Agent entrypoint, shim, or `.sdkwork/` change | `SOUL.md`, `AGENTS_SPEC.md`, `SDKWORK_WORKSPACE_SPEC.md`, `DOCUMENTATION_SPEC.md`, `TEST_SPEC.md` |
| Any authored source change | `CODE_STYLE_SPEC.md`, `NAMING_SPEC.md`, plus only the touched language or framework spec |
| Build scripts, dev runners, or `pnpm clean` | `CODE_STYLE_SPEC.md` §7, `PNPM_SCRIPT_SPEC.md`, `TYPESCRIPT_CODE_SPEC.md` when Node scripts are touched |
| Package scripts, command names, or lifecycle commands | `PNPM_SCRIPT_SPEC.md` |
| Package or release workflow | `GITHUB_WORKFLOW_SPEC.md`, `RELEASE_SPEC.md`, `SUPPLY_CHAIN_SECURITY_SPEC.md` |
| API contract, handler, or API assembly | `API_SPEC.md`, `SDK_SPEC.md`, `TEST_SPEC.md`; `WEB_FRAMEWORK_SPEC.md` and `WEB_BACKEND_SPEC.md` when HTTP runtime code is touched |
| List, search, or pagination behavior | `PAGINATION_SPEC.md`; verify with `check-pagination.mjs` |
| SDK generation or generated-client consumption | `SDK_SPEC.md`, `SDK_WORKSPACE_GENERATION_SPEC.md`, `APP_SDK_INTEGRATION_SPEC.md` |
| Source configuration, environment profiles, or `etc/` | `SOURCE_CONFIG_SPEC.md`, `CONFIG_SPEC.md`, `ENVIRONMENT_SPEC.md` |
| Application identity, runtime targets, or release metadata | `APP_MANIFEST_SPEC.md`, `APPLICATION_SPEC.md`, `DEPLOYMENT_SPEC.md` |
| Database contract, migration, or seed change | `DATABASE_SPEC.md`, `DATABASE_FRAMEWORK_SPEC.md`, `MIGRATION_SPEC.md` |
| Repository documentation, PRD, or architecture | `DOCUMENTATION_SPEC.md`, `REQUIREMENTS_SPEC.md`, `ARCHITECTURE_DECISION_SPEC.md` |
| Delete, move, overwrite, or reset files or state | `DESTRUCTIVE_OPERATION_SPEC.md`, `SOUL.md` §5, `CODE_STYLE_SPEC.md` §8 |
| Defect repair, restore, or divergence | `ROLLBACK_RESTRICTION_SPEC.md`, `SOUL.md` §5.1, `CODE_REVIEW_SPEC.md` |
| Client UI work | `FRONTEND_CODE_SPEC.md`, `FRONTEND_SPEC.md`, `UI_ARCHITECTURE_SPEC.md`, and exactly one architecture-specific UI spec |

Language-specific specs are on-demand: a Rust task loads `RUST_CODE_SPEC.md`; a TypeScript task
loads `TYPESCRIPT_CODE_SPEC.md`; a frontend task loads `FRONTEND_CODE_SPEC.md`; a Flutter task loads
`DART_CODE_SPEC.md`. Never load unrelated language specs for a scoped change.

## Code Style Rules

Follow `CODE_STYLE_SPEC.md` and `NAMING_SPEC.md` for every authored change. Match the surrounding
naming, layering, and file organization instead of introducing a second convention. Specs and
documentation use concise Markdown with RFC-style `MUST`/`SHOULD`/`MAY` where rules are normative.

Deletion is explicit and enumerated: never delete by wildcard, glob, brace expansion, recursive
walk, `git rm -r`, or `git clean -f*` (`DESTRUCTIVE_OPERATION_SPEC.md`). Defects are fixed forward;
version-control state is never moved to make a failure disappear
(`ROLLBACK_RESTRICTION_SPEC.md`). Both disciplines arrive as tool-owned managed blocks at the end of
this file — do not restate or edit them here.

## Build, Test, and Verification

No language toolchain is adopted yet, so this repository has no `package.json`, `Cargo.toml`, or
build pipeline. Repository-contract verification, which must pass on every change:

```bash
node ../sdkwork-specs/tools/audit-repository-baseline.mjs --root .
node ../sdkwork-specs/tools/check-workspace-layout.mjs --root .
node ../sdkwork-specs/tools/check-workspace-packages-layout.mjs --root . --mode enforce
node ../sdkwork-specs/tools/check-repository-docs-standard.mjs --root .
node ../sdkwork-specs/tools/check-apps-directory-index.mjs --root .
node ../sdkwork-specs/tools/check-gitignore-standard.mjs --root .
```

Release wiring is deliberately deferred. `check-agent-workflow-standard.mjs --root .` validates the
`AGENTS.md` entrypoints (which pass) and, because this root declares `repository-kind: application`,
also requires `agent.workflow.json` and `.github/workflows/package.yml`. Those two files arrive with
the first application surface, together with `agent.app.config.json` and its package targets
(`APP_MANIFEST_SPEC.md`, `GITHUB_WORKFLOW_SPEC.md`). Do not add a packaging shell that packages
nothing; add the surface first.

When a toolchain is introduced, its root scripts follow `PNPM_SCRIPT_SPEC.md`. Run only the
narrowest verification selected by the changed surface, and widen scope only when the change
crosses a contract boundary.

## Agent Execution Rules

- Do not invent standards from memory. Resolve the authority with the order above before editing.
- Do not create a standard directory that the repository does not need, and do not bypass a reserved
  directory name with a look-alike.
- Do not hand-edit generated SDK output under `sdks/`; fix the generation chain and regenerate.
- Do not commit secrets, tokens, private keys, runtime databases, or user-private state.
- Keep agent instructions here, local rules in local contracts, and normative standards in
  `sdkwork-specs`; do not duplicate a global spec body into this repository.

## Human Review Rules

Human review is required before: activating a new application surface architecture, authoring
`agent.app.config.json` or `agent.workflow.json`, changing a public API or SDK contract, deleting or
overwriting tracked content beyond the current change, adding a security or privacy exception, or
changing naming that affects other repositories. Report the exact commands run and their outcome
instead of claiming compliance without evidence.

<!-- SDKWORK-DESTRUCTIVE-OPERATION-STANDARD: v1 -->
## Destructive Operation Safety

Authority: `../sdkwork-specs/DESTRUCTIVE_OPERATION_SPEC.md`.

Deletion must be explicit, enumerated, and reviewable. Deleting by pattern instead of by named
path is forbidden. Wildcards are for read-only commands only.

- `git rm -r`, `git rm` over a directory or pattern, and `git clean -f`/`-fd`/`-fdx` are
  FORBIDDEN. A recursive `git rm` stages many deletions in one index transaction; if the process
  is interrupted (SIGTERM, timeout, sandbox kill, crash) entries are already gone from disk while
  the index is only half-written, which is silent non-atomic mass data loss.
- Delete tracked files with `rm <exact/path>` on each named path, let `git status --short`
  record the `D` entries, then stage only the enumerated paths. Commit the deletion separately
  from functional changes.
- Shell and script deletion by wildcard is FORBIDDEN: `rm -rf`/`rm -r`/`rm -f` with
  `*`/`**`/`?`/`[...]`/brace expansion, `find ... -delete`, `find ... -exec rm`,
  `find ... | xargs rm`, `for f in *; do rm ...`, `del /S /Q`, `rd /S /Q`,
  `Remove-Item -Recurse -Force` on a glob, `shutil.rmtree`, `fs.rm(dir, { recursive: true })`,
  and `rimraf` over a glob.
- A deletion MUST NOT be combined in one shell invocation with a build, install, network, or
  publish step, and MUST NOT derive its targets from an unvalidated argument, environment
  variable, or configuration value.
- Permitted narrow deletion: `rm <exact/path>`; a short literal path list owned by the tool that
  declares it; the module's own generated artifacts through its owning tool
  (`pnpm clean`, `cargo clean`) per `CODE_STYLE_SPEC.md` §7; and
  `git restore --worktree --source=HEAD -- <exact paths>`.
- Required sequence before any deletion: enumerate exact paths; confirm every path resolves inside
  the active repository or module root; classify tracked/generated/cached/unknown; prefer `rm`
  plus tracked `git status`; delete in batches of 20 or fewer with a status check between
  batches; report the removed paths and the authorizing decision.
- Request explicit human confirmation before deleting any git-tracked path, any directory tree,
  any path resolving outside the active repository root, or more than 20 paths.
- Recovery after an accidental mass deletion: clear a stale `.git/index.lock`, write the path
  list to a file INSIDE the repository (never `/tmp` on Windows, where the Git Bash path space
  and the native tool path space disagree), and run a single
  `git restore --worktree --pathspec-from-file=<repo-relative-list>`. Never loop one
  version-control call per path; the same termination cause interrupts the loop part-way.

Verification (from the repository root):

```bash
node ../sdkwork-specs/tools/sync-agent-destructive-operation-standard.mjs --root . --check
```
<!-- /SDKWORK-DESTRUCTIVE-OPERATION-STANDARD: v1 -->

<!-- SDKWORK-ROLLBACK-RESTRICTION-STANDARD: v1 -->
## Rollback Restriction And Fix-Forward Discipline

Authority: `../sdkwork-specs/ROLLBACK_RESTRICTION_SPEC.md`.

Errors are fixed forward. Version-control history is never rewound to make an error disappear.

- A rollback is any operation that moves a ref, resets the index or the working tree to an earlier
  state, discards uncommitted or committed work, or rewrites published history. It is FORBIDDEN as
  the remedy for a defect — a build failure, a type error, a lint failure, a failing test, a merge
  conflict, a runtime regression, a bad refactor, or an unclear diff. Repair forward instead, by
  adding, editing, or restoring content through a new commit.
- FORBIDDEN by an agent or a human-issued command: `git reset --hard` in any form;
  `git reset --merge`/`--keep`; `git reset <ref>` that discards staged or working-tree content;
  `git checkout -f`, `git switch -f`, `git restore --source=<ref> --worktree .`;
  `git revert` as a reflex error remedy; `git stash drop`/`clear` and `git stash pop` over a
  conflict; `git branch -D` on a branch with unmerged work; `git update-ref -d` and direct
  `.git/refs/` edits; `git reflog expire`, `git gc --prune=now`, `git prune`;
  `git commit --amend` over a pushed commit; `git rebase`, `git rebase -i`, `git rebase --onto`;
  `git filter-branch`; `git push --force`, `git push --force-with-lease`, and
  `git push --delete`.
- A rollback is never inferred from context or tone. "Fix it", "it's broken", "this is a mess",
  "start over", "just revert it", and "退回" are not rollback instructions. If the intent is
  ambiguous, STOP and ask — including whether the instruction means to discard work or to restore
  lost work, because that distinction decides the permissible operation.
- Discarding work requires a separate, explicit, human-issued instruction that names the operation,
  the target ref, the discarded span, and the reason, and that acknowledges the loss. The
  authorization must be quoted in the commit message. A standing authorization is not accepted.
- Recovery is ADDITIVE: `git restore --worktree --source=<ref> -- <exact paths>`, or
  `git checkout <good-ref> --pathspec-from-file=<repo-relative-list>` with the list written inside
  the repository. The pathspec must be an explicit enumerated list — never a directory, glob, brace
  expansion, or the repository root — and a restore is never combined with a build, install,
  publish, or commit step in the same shell invocation.
- Before a bulk restore: commit any local modification as a checkpoint; create a backup branch AND a
  tag AND a patch file and verify they point at the pre-restore state; produce a written
  three-snapshot blob comparison (damaged revision vs its parent vs the candidate older snapshot)
  that separates REPLACED files from files the damaged revision legitimately AUTHORED; restore the
  relative complement, not the whole tree; and keep the files the damaged revision added.
- Never treat a local tracking ref as evidence about a remote. Confirm with
  `git ls-remote <remote> <branch>` and record the returned object id.
- After a restore, verify by content hash rather than by reading files, re-run the gates that cover
  the restored surface, and classify each remaining failure as caused-by-the-restore or
  pre-existing. A pre-existing claim must be proven by showing the same failure at the prior
  revision with `git show <ref>:<path>`, not reasoned about. Fix forward. Never un-restore.
- Never bypass a hook, signature, or gate with `--force`, `--no-verify`, or `--no-gpg-sign` to
  land a repair.

Verification (from the repository root):

```bash
node ../sdkwork-specs/tools/sync-agent-rollback-restriction-standard.mjs --root . --check
```
<!-- /SDKWORK-ROLLBACK-RESTRICTION-STANDARD: v1 -->

<!-- SDKWORK-MAIN-BRANCH-STANDARD: v1 -->
## Main-Branch Development

Authority: `../sdkwork-specs/REPOSITORY_BASELINE_SPEC.md` section 1.

Development happens on `main`. Everything authored in this repository is committed onto `main`.

- A working tree that receives authored content MUST have `main` checked out as its current branch
  for the whole time that work is in progress. Commit onto `main` directly; do not commit onto a
  branch a later merge is expected to bring in.
- A detached HEAD MUST NOT be used as a development venue. A commit created while HEAD is detached
  from every branch is reachable only through the reflog — absent from every branch history, from a
  fresh `git clone` of this repository, and from every other working tree — so the work it carries
  is one `git gc` away from being unrecoverable. Do not check out a bare commit, a tag, or an older
  ref in order to "get a clean starting point" and commit there.
- A side branch MUST NOT be used as a development venue either. There is no long-lived feature,
  release, maintenance, or personal branch, and this repository MUST NOT accumulate local commits
  that `main` cannot reach: making them findable would then depend on a merge that may never happen.
- A checkout off `main` is legitimate only while it stays read-only — a dependency or SDK pinned to
  an explicit commit, a release artifact checkout, or a bisect. No authored change is committed there.
- A working tree found detached, or on a branch other than `main`, with work in it is a STOP, not a
  cleanup. Do not move refs, do not rewrite history, and do not discard the commits. Report the
  branch, the commits, and the state, and let a human decide: moving commits onto `main` and
  discarding work are both governed by `../sdkwork-specs/DESTRUCTIVE_OPERATION_SPEC.md` and
  `../sdkwork-specs/ROLLBACK_RESTRICTION_SPEC.md`.

Verification (from the repository root):

```bash
node ../sdkwork-specs/tools/audit-repository-baseline.mjs --root . --only branch-main
node ../sdkwork-specs/tools/sync-agent-main-branch-standard.mjs --root . --check
```

The first fails when the current branch is anything other than `main`, and reports a detached HEAD
as `detached`. The second fails when this block is out of date.
<!-- /SDKWORK-MAIN-BRANCH-STANDARD: v1 -->
