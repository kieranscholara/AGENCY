# Product and Engineering Roadmap

**Status:** Planning, not completion proof. Milestones only move to Done after documented acceptance evidence in `PROJECT_STATE.md`.

| Milestone | Deliverable | Exit criteria | Status |
| --- | --- | --- | --- |
| M0 | Repo, run instructions, docs, CI baseline | App runs locally; documented checks; private repo | Not verified |
| M1 | Secure tenant foundation | Auth, organisations, role policies, DB RLS, negative isolation tests | Not started |
| M2 | Customer + AC equipment registry | Tenant-safe CRUD, addresses/equipment relations, validation | Not started |
| M3 | Jobs + scheduling | Assignment, calendar, role-dependent visibility, status transitions | Not started |
| M4 | Technician reports + photos | Mobile flow, secure uploads, history, service report | Not started |
| M5 | Due dates + email reminders | Consent settings, durable jobs, idempotent retries | Not started |
| M6 | Customer import + pilot onboarding | CSV preview, reconciliation, approved pilot run | Not started |
| M7 | Billing + commercial readiness | Stripe verified webhooks, tested releases, backups, privacy/support | Not started |
| M8 | Integrations and advanced features | Prioritised based on repeated paid customer needs | Deferred |

## Milestone operating rule

For each milestone:
1. Write a concise technical plan and acceptance scenarios.
2. Obtain approval for schema/security/API changes.
3. Build in small PRs with tests.
4. Verify on staging and record results.
5. Update project state and release documentation.

## Release strategy

Initial beta is **not** automatically production-ready. Only onboard real customers after tenant isolation, private storage, backup/recovery and permission tests pass and relevant security review is completed.

## Research before committing resources

Interview target AC companies about their actual schedule, number of technicians, field connectivity, equipment records, recurrence patterns, current software and pricing expectations.


## Pilot fast track vs full roadmap

For a client 3–4 weeks away, use `docs/FOUR_WEEK_PILOT_PLAN.md` and `docs/SCOPED_SPRINT_BACKLOG.md` as a narrow, conditional release strategy. M7 Stripe Billing and M8 external system connectors may be **deferred for a contract-supported pilot**, not eliminated from long-term roadmap. Do not compromise M1 tenant security, tested backups or client acceptance.
