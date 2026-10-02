---
name: multi-repo-product-workflow
description: Manage a product split across documentation or coordination, backend and frontend repositories. Use for repository orchestration, contract-first development, local milestone commits, deferred push/PR delivery, cross-repository handoffs, testing and stable integration.
---

# Multi-repository product workflow

Use this workflow when one product is divided into independent repositories, typically:

- documentation/coordination repository: requirements, architecture, decisions, work items and source inventory;
- backend repository: domain rules, persistence, imports, validation, APIs and release controls;
- frontend repository: user interface, API client, accessibility, browser behavior and presentation.

Project-specific repositories, commands and policies belong in each repository's `AGENTS.md` or in a small project profile. Do not hard-code one project's names into this reusable skill.

## Repository and workspace boundaries

1. Work from a dedicated workspace containing only the related repositories. Do not initialize a parent repository, add submodules or scan unrelated personal directories.
2. Keep the repositories independent. Cross-repository work is coordinated through explicit contracts, linked work items and handoffs.
3. Read the local `AGENTS.md`, current branch, `git status --short`, manifests and relevant documentation before editing.
4. Treat the documentation repository as the coordination authority for product decisions, not as a second application implementation.
5. Let each repository own its own runtime, dependencies, tests and development Compose configuration.

## Ownership and contract-first order

- Documentation/coordination defines the problem, scope, non-goals, data/API contract, acceptance criteria, decisions and open questions.
- Backend implements the authoritative domain behavior and API after the contract is explicit.
- Frontend consumes the agreed API and implements presentation, accessibility and browser behavior. It must not recreate backend calculations or disclosure rules.
- For a cross-repository feature, coordinate in this order:

  `decision/contract → backend implementation → frontend adaptation → integration verification → documentation update`

- Parallelize only independent work. Do not allow multiple agents to edit the same repository/worktree concurrently.
- A feature spanning three repositories is not one atomic Git commit. Track each repository's branch and commit separately.

## Local-first Git lifecycle

Use deferred remote delivery as the default.

### During development

1. Create a task branch in each repository that will change.
2. Make small, coherent changes.
3. Run focused checks after each milestone.
4. Create local atomic commits after verified milestones so work can be reviewed or rolled back locally.
5. Keep commits local by default. Do not push every commit and do not open a PR for every intermediate experiment.
6. Record the local commit SHA, repository, checks and dependency state in the work-item handoff.

A local commit is a checkpoint, not a publication. The absence of a push does not mean the work is uncommitted.

### Stabilization checkpoint

Push only after the affected repositories reach a stable checkpoint, unless the user explicitly asks for an earlier remote backup or collaboration.

Before pushing:

- complete the planned implementation for the current slice;
- run the relevant unit, integration, build, lint, security and browser checks;
- inspect `git diff`, `git diff --check` and the commit range;
- verify that secrets, private datasets, generated artefacts and unrelated edits are absent;
- verify cross-repository API/data compatibility;
- update the work-item summary with exact commands and results;
- decide the push order, normally documentation/contract first, backend second and frontend third.

Then push the task branches and open or update PRs as one deliberate delivery step. Keep local commits visible and meaningful; do not create a single opaque mega-commit merely because the push was deferred.

### Exceptions and limits

Push earlier only when explicitly requested, when a remote backup is materially needed, or when another contributor/CI must consume the branch. State the reason in the handoff.

Never:

- force-push or rewrite shared history without explicit authorization;
- merge a PR, deploy, publish official statistics or delete a branch without authorization;
- use a PR as a substitute for local verification;
- claim remote CI or review ran when the branch was not pushed.

## Progressive work loop

1. Inspect and classify the task: documentation, backend, frontend or cross-repository.
2. Create/update one bounded work item with goal, scope, non-goals, owner, acceptance criteria and dependencies.
3. Establish or update the contract in the coordination repository.
4. Implement the smallest useful backend slice and add regression tests.
5. Adapt the frontend only to the explicit contract and add UI/browser tests.
6. Run checks, review the diff and commit locally in each repository.
7. Reconcile the repositories locally, documenting exact branch/commit relationships.
8. Stabilize, then push and open/update PRs deliberately.
9. Review the final PRs and rescan all repositories before merge.

## Data, security and release boundaries

- Keep secrets in ignored runtime files; never commit `.env`, credentials or tokens.
- Keep restricted source data, workbooks, personal data and private operational details outside Git, logs, issues, screenshots, fixtures and build contexts.
- Keep raw inputs, normalized facts, validation results and approved releases as distinct states.
- Do not allow an LLM or frontend code to originate official figures, bypass validation or approve publication.
- Report missing, suppressed and zero values distinctly.
- Apply project-specific privacy, disclosure and publication approvals before exposing data.

## Tool and quality discovery

Discover actual availability of Pi/PiWorkflow, Herdr, GGA, Gentle/Engram, Pi VCC, Wizard-AI and other optional tools. Record installed, missing or incompatible capabilities. Do not invent commands, sessions, model availability or completed reviews.

Report checks as `PASS`, `FAIL`, `BLOCKED` or `NOT RUN`. A mock test proves only the mocked behavior. A successful import is not approval for publication. If a required tool or runtime is unavailable, preserve the work and state the exact blocker.

## Handoff contract

End each repository task with a compact handoff:

```text
Status: PASS | FAIL | BLOCKED | NOT RUN
Repository and owner:
Branch:
Local commit(s):
Remote push/PR: deferred | pushed | not requested
Goal and scope:
Contract/API/data assumptions:
Changed paths:
Checks and exact results:
Cross-repository dependencies:
Open blockers:
Next action:
```

Keep durable decisions in versioned documentation. Use memory only as supplementary context.
