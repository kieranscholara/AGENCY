# 4-Week Pilot Release Plan — Conditional

**Status: PLAN, no dates committed, no live client confirmed.** Starting point unknown. Realistic only for a narrow, web-based MVP and rapid decisions. Launch means restricted production pilot, not "feature-complete enterprise SaaS". Use test/staging before live records. A qualified reviewer must evaluate security/data controls before real users.

## Default pilot scope

1. Owner and technician accounts with separate permissions and securely isolated company workspaces.
2. Customer → service address → AC unit registry (no complex parts/inventory).
3. Create/schedule/assign job; technician can view assigned jobs on mobile.
4. Complete checklist/notes/report and maintain auditable service history.
5. CSV import **if first client supplies real export early**; manual entry fallback for very small sample.
6. Production hosting, monitoring, backup/restore, client signoff, support and data export strategy.

**Explicitly deferred** unless contract requires: Stripe subscriptions (manual invoice pilot acceptable), automated SMS/WhatsApp, two-way CRM/accounting sync, AI, advanced route optimisation, native mobile/offline, stock control, custom report builders, multi-country tax and platform-superadmin impersonation.

## Week 1 — Discovery + secure foundation

**Client:** approve one-page SOW, provide decision maker and anonymised sample data, confirm auth/roles and critical reports.

**Engineering:** audit actual repo and environment; verify framework, set up dev/staging/prod separation; write data/API/role contracts; implement auth/org/membership and migrations+RLS; create two-tenant test fixture; establish CI lint/types/build/tests; review database constraints with human.

**Exit:** local/staging auth works, two companies cannot see each other's data even with guessed IDs, reviewer approves design, scope frozen. **If fail: delay data import and launch.**

## Week 2 — Core office workflow

Build customer/site/AC unit CRUD, paginated search, schedule/assign jobs, server validation, transactional writes and audit; responsive office dashboard. Use synthetic data and error cases. Staging demo with client at week end.

**Exit:** office user completes customer→unit→job without manual DB intervention; automated role/tenant negative tests pass; client accepts workflow naming and data fields.

## Week 3 — Technician flow + migration

Implement mobile job list, start/complete/report, private photo upload only if needed, service history and simple PDF only if signed scope. Build CSV staging, preview, dedupe and reconciliation if real data export exists. Perform limited test import into **staging only**. Run accessibility/phone checks, concurrent job edits, DST dates.

**Exit:** full start-to-finish flow demonstrated on phone; import reconciles or manual migration is approved; no high-severity functional or security bugs.

## Week 4 — Hardening and restricted production pilot

Finalize permission and storage reviews, dependency/secret scan, E2E acceptance, performance smoke test, backups **and isolated restore drill**, support/incident runbook, deployment rollback and operator alerts. Client UAT, approved production credentials, rehearsed migrations, supervised data import, soft launch to limited users, monitor daily.

**Exit:** release gate in `PILOT_ACCEPTANCE_TESTS.md` and `RELEASE_RUNBOOK.md` all passed, client signed scope and acceptance. If not, do **not** silently lower critical gates; reduce functionality or postpone launch.

## Owner / schedule dependencies

Client approver answers questions in <=1 business day (target, not contractual); access to current systems and sample data in Week 1; founder available to test daily; optional senior security review scheduled early; hosting and privacy agreements arranged before Week 4.

## If only 3 weeks

Defer photo uploads, CSV importer (use validated manual entry for small client), PDF generation, automated reminders and SaaS billing. Keep auth/RLS, backup/restore, tests, staging UAT and controlled deploy. If client cannot accept that narrow scope, negotiate delivery date.

## Metrics for pilot

Job creation-to-completion success rate; number of reconciled customer/equipment records; permission test coverage; error rate and production incidents; mobile task usability; support requests. Baselines/targets are TBD pending discovery.
