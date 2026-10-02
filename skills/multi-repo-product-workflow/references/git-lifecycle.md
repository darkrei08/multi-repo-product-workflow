# Local-first Git lifecycle

The default delivery policy is:

`edit → focused check → local atomic commit → cross-repository stabilization → full verification → push/PR`

Commit locally at meaningful milestones. Do not push every commit merely to preserve history; local commits already provide rollback and review checkpoints. Do not wait until the end to create the first commit, because a single late mega-commit destroys useful history.

Push before stabilization only when remote backup, CI, collaboration or an explicit user request justifies it. State that exception in the work item.

For multiple repositories, compare local refs and contracts before pushing. Push in dependency order when practical:

1. documentation/contract;
2. backend/API;
3. frontend/client.

A pushed branch may still be unmerged. Treat remote publication, PR review, merge, deployment and statistical release as separate gates.
