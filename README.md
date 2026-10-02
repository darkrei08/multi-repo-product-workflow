# Multi-repo Product Workflow

Reusable skill for projects split across independent documentation/coordination, backend and frontend repositories.

## Install with `npx skills`

This repository follows the same installation mechanism as
[Engineering Excellence](https://github.com/darkrei08/Engineering-Excellence):

```bash
npx skills@latest add darkrei08/multi-repo-product-workflow --skill multi-repo-product-workflow --global --agent pi --copy --yes
```

Keep the command on one line. Replace `--agent pi` with another supported
agent (for example `claude`, `gemini`, `cursor` or `antigravity`) when
needed. The `--global` flag installs the skill in the agent's global skills
directory; omit it for a project-local installation.

The installable source is
`skills/multi-repo-product-workflow/`. The root `SKILL.md` and
`references/` paths remain as compatibility links for direct repository
consumers and existing project documentation.

## Included

- `skills/multi-repo-product-workflow/SKILL.md`: canonical skill loaded by `npx skills`.
- `skills/multi-repo-product-workflow/references/git-lifecycle.md`: local-first commit and delivery policy.
- `agents/openai.yaml`: optional skill metadata for OpenAI-compatible agents.
- Root `SKILL.md`: compatibility copy for direct linking.

## Core delivery policy

```text
inspect → define contract → implement → test → local atomic commits
→ stabilize all affected repositories → verify → push/PR
```

Commits are created locally at meaningful milestones for rollback and review. Intermediate commits are not pushed automatically. Push only at a stable checkpoint, or earlier when remote backup, CI, collaboration or an explicit request requires it.

## Use in a project

Load `SKILL.md` together with the project's local `AGENTS.md`. Keep project-specific repository names, commands, API contracts, data rules and release policies in the project profile; do not hard-code them into this reusable skill.

The skill does not store secrets or natural-language directives in `.env`. Environment files are reserved for runtime configuration.
