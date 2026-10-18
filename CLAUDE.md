# Claude Code Project Instructions

Read and follow [`AGENTS.md`](AGENTS.md) first. Those are the canonical shared instructions for Claude Code, Codex, and other coding assistants.

Before editing, inspect the repository and read:
- `docs/PROJECT_STATE.md` — verified current state
- `docs/ARCHITECTURE.md` — intended technical boundaries
- `docs/SECURITY.md` — tenant, auth, and file isolation
- `docs/REQUIREMENTS.md` — acceptance criteria for current milestone

Do not generate the complete product from one prompt. Propose a small, testable plan and wait for approval for architectural, database, security, billing, or deployment changes.

At task completion report exact checks run, state what was *not* verified, and update the project state/handoff where relevant. No automatic production deployment.
