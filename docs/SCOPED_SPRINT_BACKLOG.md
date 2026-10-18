# 4-Week Engineering Backlog — Ordered and Testable

**Status: proposed, not estimates or completed tickets.** Convert each item to a GitHub Issue with dependencies and acceptance test. Avoid concurrent edits to the same schema/policy module by multiple agents.

## Week 1 / P0 foundation

- **S01** Audit repo and `package.json`, Supabase, env and existing tests; update PROJECT_STATE with commands/evidence.
- **S02** Client-approved scope/user roles/one full workflow; mark unclear integrations deferred.
- **S03** Create organisations + members migrations with correct signup/invite flow and secure role assignment.
- **S04** Add customers test table with tenant FK/RLS as first vertical slice; negative access tests for Org A/B.
- **S05** CI lint/types/test/build and staging environment. Reviewer validates S03–S04.

## Week 2 / P0 office flow

- **S06** Customers with search/validation/archival; service addresses; tenant constraints.
- **S07** Equipment records and linking to service address; tests for wrong-org IDs.
- **S08** Jobs create/list/assign/reschedule; state + optimistic version, permission checks.
- **S09** Office UI responsive forms with loading/error states, staging client demo.

## Week 3 / P0 technician and migration

- **S10** Technician assigned job list/detail and state transition; mobile testing.
- **S11** Report checklist and completion transaction with retry protection.
- **S12** Service history view/audit records and selected file upload if required.
- **S13** CSV import preview/dedupe/commit/reconcile if client gave export; otherwise manual migration pathway.
- **S14** Full E2E journey across two tenant accounts and wrong-role negative tests.

## Week 4 / P0 go-live controls

- **S15** Staging UAT; critical defect fixing; signed import reconciliation.
- **S16** Security review on RLS, FKs, Auth, private files, secrets, API checks.
- **S17** Backup+storage restore rehearsal, deploy rollback and alerts.
- **S18** Production launch with limited users, smoke tests and client signoff.

## Cut first if schedule slips

P2: branding polish, analytics, AI features. P1: advanced dashboards, PDF theming, automated reminders, multi-staff per job, extensive import automation, billing self-service. P0 NEVER cut: authentication/tenant isolation, data integrity, basic tests, recovery, user acceptance and operational support.

## Must agree at start

Does the first client actually work in AC servicing? Is there an existing codebase? Does client require existing system integration before launch? Who can approve each week? Unknowns may make this 4-week plan infeasible.
