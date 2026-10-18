# How to Install This Markdown Documentation Pack

**Read before copying.** This is a starter pack of project specifications and engineering rules, not working application code.

## Safe installation

1. Make a Git commit or backup of your current application.
2. Extract the archive. Its top-level folder is `ac-service-manager/`.
3. Copy its Markdown files and nested `.github/` Markdown template into the **root of your actual repo**, preserving relative paths.
4. If your repo already has a `README.md`, `AGENTS.md`, `CLAUDE.md`, or `.github/PULL_REQUEST_TEMPLATE.md`, **merge content instead of blindly overwriting it**.
5. Read `docs/OPEN_QUESTIONS.md`. Update assumptions, especially whether the app is Next.js/Supabase or Lovable-generated.
6. Update `docs/PROJECT_STATE.md` with only facts verified by inspecting/running the repository.
7. Commit docs in a branch and review before merging to `main`.

## What to read first

`AGENTS.md` → `docs/PRODUCT.md` → `docs/ARCHITECTURE.md` → `docs/SECURITY.md` → `docs/PROJECT_STATE.md` → `docs/ROADMAP.md`.

## Your first safe agent instruction

> Read AGENTS.md and docs/START_HERE.md. Inspect the repository, package.json, authentication, database and current tests. Without changing code or database state, compare actual implementation with docs/ARCHITECTURE.md and docs/PROJECT_STATE.md. Identify incorrect assumptions, report security risks and propose the smallest M1 foundation task with acceptance criteria. Do not claim features are complete unless verified.

## Important

These files intentionally mark much of the product as **proposed or unverified**. Don't remove those qualifiers until a human has confirmed the corresponding implementation.


## Updated reading order for urgent 3–4 week pilot

Read `docs/FOUR_WEEK_DECISION_LOG.md` with client/owner first, then `docs/FOUR_WEEK_PILOT_PLAN.md`, `docs/GET_STARTED_WITH_CODEX.md`, detailed API/tenant docs and the `docs/PILOT_ACCEPTANCE_TESTS.md`. Do not copy an entire directory over existing code without reviewing diffs and merging collisions.
