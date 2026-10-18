# First Instruction to Codex or Claude Code — Read-only Audit

Before implementing anything, use the following task. This document doesn't create code or prove that the stack exists.

> You are the senior full-stack engineer for a Next.js/Supabase **proposed** multi-tenant AC Service Manager. Inspect this actual repository, branch, package.json, migrations, Supabase configuration, authentication, storage, API routes, tests, CI and available environments. Read AGENTS.md, docs/PROJECT_STATE.md, docs/FOUR_WEEK_DECISION_LOG.md, docs/SYSTEM_COMMUNICATION.md, docs/FRONTEND_BACKEND_CONTRACT.md, docs/API_SPECIFICATION.md, docs/DATABASE_IMPLEMENTATION.md, docs/AUTHORIZATION_MATRIX.md, docs/FOUR_WEEK_PILOT_PLAN.md. Do not modify code or connect to production. Produce a fact-vs-assumption audit, contradictions, missing access, a security risk list and a **first 48-hour plan** to get one end-to-end tenant-safe customer create working with automated negative tests. For each proposed change state target files, DB migrations, exact commands and success criteria. Ask for permission before implementing changes.

## First implementation task after audit is approved

Create/review organisations, membership, customer entity, DB FK/RLS, protected create/list customer API and simple UI with two-tenant test fixtures. Tests must prove cross-tenant reads/writes fail. Do not build the full dashboard, Stripe or integrations yet.

## Milestone evidence

Append real outcomes into `PROJECT_STATE.md`: git SHA, actual `npm` scripts run and output, Supabase migration identifiers, test names, screenshot/staging URL where appropriate, reviewer and open risks. "It should work" is not evidence.
