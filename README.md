# dev-skills

Reusable AI coding-agent skills for software development workflows.

This repo is a small catalog of skills that are useful across projects. Each
skill keeps its own workflow details in its directory.

## Skills

| Skill | Purpose |
|---|---|
| [`infra-product-docs`](infra-product-docs/SKILL.md) | Create, audit, reorganize, and maintain documentation for infrastructure and developer products. |
| [`pr-doc-sync`](pr-doc-sync/SKILL.md) | Check whether a pull request should update project docs before it is considered complete. |

## Install

Install a single skill by name:

```bash
npx skills add shenli/dev-skills@<skill-name> -g
```

Skill-specific setup lives in each skill's `SKILL.md`.

## Update

Update installed skills:

```bash
npx skills update
```

Check what would change before updating:

```bash
npx skills check
```

To force-refresh this skill from GitHub, run the install command again:

```bash
npx skills add shenli/dev-skills@<skill-name> -g
```

## Repository Layout

```text
<skill-name>/
  SKILL.md
  agents/openai.yaml   # optional UI metadata
```

## Adding Skills

Keep new skills focused and portable:

- put reusable workflow logic in the skill
- put project-specific policy in the consuming repo's agent instructions
- avoid adding repo-specific paths or product names to a general skill
- keep `SKILL.md` concise enough to load into an agent context
