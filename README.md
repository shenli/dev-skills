# dev-skills

Reusable AI coding-agent skills for developer workflows.

## Skills

- [`pr-doc-sync`](pr-doc-sync/SKILL.md) - checks whether a pull request should
  update design, roadmap, architecture, API, operations, release, or
  implementation-status docs before the PR is considered complete.

## Install

```bash
npx skills add shenli/dev-skills@pr-doc-sync -g
```

## Repo Configuration

`pr-doc-sync` is intentionally general. Each repository should define its own
documentation targets in `AGENTS.md` or equivalent repo instructions.

Example:

```markdown
## PR Documentation Sync

When finishing, pushing, or opening a pull request, check whether the change
updates product behavior, architecture, operations, API/SDK surface,
implementation status, support boundaries, or known limitations.

If it does, update the relevant docs before calling the PR complete:

- Design and implementation status: `docs/architecture/current-design.md`
- Product progress and gaps: `docs/product-roadmap.md`
- API and SDK behavior: `docs/reference/api-sdk.md`
- Operations and deployment behavior: `docs/operations/`

If docs are not needed, state why in the PR summary or final response.
```
