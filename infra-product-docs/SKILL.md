---
name: infra-product-docs
description: Use when creating, auditing, reorganizing, renaming, consolidating, or updating documentation for infrastructure and developer products, including product thesis, design, architecture, roadmap, operations, API, SDK, runtime, reliability, and implementation-status docs.
---

# Infra Product Docs

Use this skill to make docs for infrastructure and developer products clear,
current, and useful to both builders and operators.

## Install

```bash
npx skills add shenli/dev-skills@infra-product-docs -g
```

## Principles

- Prefer purpose-first information architecture. One doc should have one main
  job and one primary audience.
- Do not use `architecture` as a catch-all. Separate product intent, design
  contracts, implementation architecture, operations, reference, and roadmap
  material when they answer different questions.
- Make current status explicit: `Implemented`, `Partial`, `Planned`,
  `Design note`, `Deprecated`, or `Not supported`.
- Separate current behavior from future direction. A reader should not have to
  infer whether a feature exists.
- Quantify infrastructure claims. Use concrete limits, workloads, validation
  commands, scale assumptions, failure modes, and cost or latency tradeoffs
  where possible. If unknown, state the measurement needed.
- Name files by durable purpose in lower-kebab-case, not by milestone,
  temporary initiative, or vague scope.
- Consolidate docs only when they answer the same question for the same
  audience. Otherwise, add a short map section that explains how the docs fit
  together.
- Keep operational complexity visible. Infra docs should expose deployment
  assumptions, observability, rollback, migration, and support boundaries.

## Common Doc Types

Use these purposes as a starting taxonomy:

| Doc Type | Primary Question | Typical Contents |
|---|---|---|
| Product thesis | Why should this product exist? | Audience, problem, position, non-goals, success criteria |
| Design | What behavior and contracts does the product commit to? | Concepts, lifecycle, semantics, status, gaps |
| Architecture | How is the system implemented? | Components, data flow, request flow, state, dependencies |
| Component design | How does one subsystem work? | Scope, invariants, alternatives, limits, open questions |
| Roadmap | What is done and what remains? | Implemented work, gaps, priority, sequencing |
| Reference | Exactly how do users call it? | API, SDK, CLI, wire protocol, compatibility, errors |
| Operations | How is it run and debugged? | Deployment, config, metrics, alerts, runbooks, rollback |

## Workflow

1. Inventory existing docs and headings:

   ```bash
   find docs -maxdepth 3 -type f -name '*.md' | sort
   rg -n '^#{1,3} ' docs
   ```

2. Classify each doc by purpose, audience, and status. Mark docs that mix
   product, design, architecture, operations, and roadmap concerns.

3. Identify overlaps and gaps:

   - duplicate explanations with different status claims
   - future design described as current behavior
   - component docs with no parent map
   - implementation docs missing operational limits
   - roadmap docs that do not say what is already implemented
   - reference docs that omit unsupported behavior or compatibility boundaries

4. Choose the smallest useful reorganization:

   - rename unclear files to lower-kebab-case purpose names
   - merge docs that serve the same audience and question
   - keep separate component docs when each has a distinct subsystem boundary
   - add a map section to a parent doc when related docs should stay separate
   - delete stale docs only when their useful content has been moved

5. Update all links and repo entry points:

   - `README.md`
   - `docs/README.md`
   - contributor or agent instructions
   - relative links inside changed docs

6. Validate before finishing:

   ```bash
   rg -n 'old/path|old-file-name' README.md docs
   git diff --check
   ```

   If the repo has a Markdown link checker, run it.

## Component Map Pattern

For related component docs, add a short map to the parent design doc:

```markdown
## Component Design Map

- `control-plane.md` covers configuration, coordination, policy, and lifecycle
  decisions.
- `data-plane.md` covers request execution, runtime behavior, and hot-path
  performance.
- `operations.md` covers deployment, observability, failure handling, and
  rollback procedures.
```

Use a map when the docs are related but should remain separate because they
have different scopes or readers.

## Closeout

When done, report:

```markdown
Docs:
- Renamed: <old> -> <new>
- Merged: <old> into <new>
- Updated links: <entry points>
- Validation: <commands run>
```

If no doc changes were made, state the reason and any remaining docs risk.
