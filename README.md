# Multi-repo Product Workflow

Reusable skill for projects split across independent documentation/coordination, backend and frontend repositories.

## Included

- `SKILL.md`: contract-first orchestration and repository ownership.
- `references/git-lifecycle.md`: local-first commits with deferred push/PR delivery.
- `agents/openai.yaml`: optional skill metadata.

## Core delivery policy

```text
inspect → define contract → implement → test → local atomic commits
→ stabilize all affected repositories → verify → push/PR
```

Commits are created locally at meaningful milestones for rollback and review. Intermediate commits are not pushed automatically. Push only at a stable checkpoint, or earlier when remote backup, CI, collaboration or an explicit request requires it.

## Use in a project

Load `SKILL.md` together with the project's local `AGENTS.md`. Keep project-specific repository names, commands, API contracts, data rules and release policies in the project profile; do not hard-code them into this reusable skill.

The skill does not store secrets or natural-language directives in `.env`. Environment files are reserved for runtime configuration.
