# Instructions for Coding Agents

**Scope:** All agent work in this repository. The human owner is the final decision-maker. Treat these rules as project requirements, not proof that they have been implemented.

## At the start of every task

1. Read `README.md`, `docs/PRODUCT.md`, `docs/ARCHITECTURE.md`, `docs/PROJECT_STATE.md`, and the relevant domain documents.
2. Inspect the real repository and existing tests. Do not assume the proposed stack is already installed or working.
3. State the objective, affected files, acceptance criteria, risks, and intended verification before a substantial change.
4. Ask for approval before changing data models, authentication, tenant boundaries, billing, production configuration, dependencies, or overall architecture.

## Architecture boundaries

- Prefer a **modular monolith**, not microservices, for the initial SaaS.
- Keep React UI/presentation separate from server-side business logic and database access.
- Reuse validated shared service functions for operations initiated by forms, API handlers, or jobs.
- Use a canonical company/organisation identifier, but derive and **validate** permissions server-side; never trust an organisation ID merely because it appears in the request.
- All tenant data must have enforced tenant isolation, including database rows, files, job queues, logs, and API results.
- An agent may propose a library, but should explain the problem solved and avoid unnecessary dependencies.

## Security invariants

- Never expose `service_role` / Supabase secret keys, Stripe secret keys, or integration tokens in a browser bundle or GitHub.
- Never disable or broadly weaken RLS to make a query work.
- Use verified authentication, explicit authorisation, input validation, tenant-safe relationships, and least privilege.
- Never perform an admin-only action based on a user-editable role claim.
- Require provider webhook signature verification, idempotency, and safe secret storage.
- Never operate on real client data or contact real customers during testing without explicit approval.
- No autonomous production deployments, irreversible migrations, access to live credentials, or unreviewed external messages.

## Development workflow

- Keep changes small and scoped to one issue/milestone.
- Add/update unit and integration tests, especially for permissions and tenant isolation.
- Run available lint, typecheck, relevant tests, and build; report actual command outputs and failures.
- Do not claim tests passed unless they were run.
- Never bypass failures by deleting tests, suppressing errors, or removing security checks without approval.
- Prefer parameterised database queries, transactions for multi-record operations, and clear error handling.
- Preserve migration history; never silently rewrite already-applied production migrations.
- Avoid committing `.env*` files containing secrets, dumps, personal data, or customer assets.

## Completion and handoff

Provide: changed files, behavioural summary, tests run/results, remaining risks, unresolved questions, and the next safe action. Update `docs/PROJECT_STATE.md`, `docs/DECISIONS.md` if applicable, and a concise handoff note under `docs/handoffs/` for substantial sessions.

## Conflict resolution

1. Security invariants and explicit user requirements.
2. Actual code, executed tests, and database schema for **current behaviour**.
3. Approved ADRs and architecture contracts for **intended direction**.
4. General documentation and agent suggestions.

If sources conflict, flag the discrepancy; do not silently select whichever is easier.
