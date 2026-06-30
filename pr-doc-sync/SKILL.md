---
name: pr-doc-sync
description: Use when finishing, pushing, opening, or preparing a pull request. Ensures relevant design, roadmap, architecture, operations, API, changelog, release, and implementation-status docs are updated according to repo instructions before the PR is considered complete.
---

# PR Doc Sync

Before calling a PR complete, check whether the change affects user-visible
behavior, architecture, APIs, operations, deployment, feature progress, known
limitations, or implementation status.

## Install

```bash
npx skills add shenli/dev-skills@pr-doc-sync -g
```

## Find Repo Doc Targets

Read repo guidance first:

- `AGENTS.md`
- repo-local agent or Codex instructions, if present
- `docs/README.md`, `CONTRIBUTING.md`, or release docs if repo guidance is
  missing or unclear

Look for configured design, roadmap, architecture, operations, API, release,
changelog, or implementation-status docs.

If repo guidance names doc targets, use those. If not, infer likely docs from
paths such as:

- `docs/architecture/*`
- `docs/design*`
- `docs/roadmap*`
- `docs/reference/*`
- `docs/operations/*`
- `CHANGELOG.md`
- `README.md`

## Decide

Update docs when the PR changes:

- public behavior
- API, SDK, CLI, or wire-protocol surface
- architecture or runtime semantics
- deployment, operations, observability, or support workflows
- feature implementation status
- roadmap progress or remaining gaps
- known limitations, non-goals, or support boundaries

Docs may be skipped for pure refactors, tests, formatting, dependency bumps, or
internal cleanup that does not change behavior or status.

## Check The Diff

Use the merge base when available:

```bash
git diff --name-only $(git merge-base HEAD origin/main)..HEAD
git diff --stat $(git merge-base HEAD origin/main)..HEAD
```

If the base branch is not `origin/main`, use the branch the PR targets.

Inspect changed files that might imply doc changes. Do not rely only on file
names when behavior could have changed.

## Closeout

Before final response, PR creation, or merge readiness:

```bash
git diff --check
```

Report one of:

```markdown
Docs:
- Updated: <paths>
```

or:

```markdown
Docs:
- Not needed: <short reason>
```

If behavior changed and no configured docs were updated, stop and update the
docs before calling the PR complete.

## Suggested Repo Configuration

Add repo-specific targets to `AGENTS.md` or equivalent agent instructions:

```markdown
## PR Documentation Sync

When finishing, pushing, or opening a pull request, check whether the change
updates product behavior, architecture, operations, API/SDK surface,
implementation status, support boundaries, or known limitations.

If it does, update the relevant docs before calling the PR complete:

- Design and implementation status: `<design-doc-path>`
- Product progress and gaps: `<roadmap-doc-path>`
- API, SDK, CLI, or protocol behavior: `<reference-doc-path>`
- Operations and deployment behavior: `<operations-doc-path-or-dir>`

If docs are not needed, state why in the PR summary or final response.
```
