# Agency-Style Development Workflow for This Product

## Issue lifecycle

`Backlog → Ready → In progress → Review → Tested on staging → Done`

A Ready issue has user value, non-goals, acceptance checks, dependencies and data/security impact. Avoid starting implementation with vague instructions such as "build the entire dashboard".

## Standard implementation loop

1. Human chooses priority and approves scope.
2. AI architect reviews actual code/docs and proposes minimal change plan.
3. Human approves changes touching architecture, DB, permissions, billing or deploy.
4. Builder (Codex/Claude Code) implements in feature branch with tests.
5. Separate reviewer checks correctness, maintainability, security and regressions.
6. CI runs lint/typecheck/tests/build and relevant tenant-isolation suite.
7. Staging smoke test and (when applicable) client acceptance.
8. Human approves merge/production release.
9. Update docs/PROJECT_STATE and handoff; document ADR if decision changed.

## Source of truth

GitHub repository, migration history, actual tests and approved architecture docs. An AI tool's conversational memory or ECC memory is supplemental, not the source of truth.

## Client-facing professionalism

For future bespoke projects, use separate repos/databases/deployments/secrets per client and explicit source-code/IP terms. For this SaaS, organisations share the application but data is isolated. Never copy unrelated client private code or information between repositories.

## AI usage safeguards

Do not give agents unbounded production access, client secrets, or automatic deployment permission. Human accountability and review remain mandatory. Record third-party agent/plugin permissions and security implications before installation.

## Definition of done

Acceptance criteria met, tests executed, migration implications handled, UI states checked, docs updated, no unresolved blocking security issue, and any necessary human approval recorded.
