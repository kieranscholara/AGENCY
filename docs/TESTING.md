# Test Strategy and Quality Gates

**Status:** Proposed policy. Actual test framework/commands are unknown until inspected.

## Test pyramid

- **Unit:** date/maintenance interval logic, permissions helpers, parsers, status transitions, price/plan calculations.
- **Integration:** repository queries, database constraints and RLS using dedicated test DB/users; uploads; invitation flow; webhook idempotency.
- **E2E (Playwright or equivalent):** owner onboarding, manager creates job, technician completes report, cross-tenant access denied.
- **Manual:** responsive/mobile service flow, keyboard use, PDF quality, real-world pilot acceptance.

## Mandatory multi-tenant tests

1. Organisation A user cannot read/list/change/delete Organisation B resources.
2. Organisation A cannot insert a job referencing Organisation B's customer/equipment.
3. Technicians cannot access unrelated private records and files.
4. Revoked membership and changed roles affect subsequent requests.
5. Unauthenticated access fails; query-parameter and guessed ID attacks fail.
6. Admin/service worker cannot create accidental unscoped data leaks.
7. Private storage download and upload policies reject guessed cross-org paths.

## Workflow tests

- Creating customer with validated fields; duplicates/archival policies.
- Scheduling invalid time/status transitions, changed assignment, conflict handling.
- Report completion must not lose prior history.
- Reminder delivery safe on retries, timezone boundaries and opt-outs.
- Import validation, duplicate handling, partial failure and reconciliation.
- Stripe signature, duplicate/out-of-order events, cancellations and plan enforcement when implemented.

## Pull request checks

Required before merge (once configured): lint, TypeScript typecheck, tests, production build, migration checks, dependency and secret scans. Enforce via branch protection; no bypass to achieve green status.

## Test evidence format

```text
Command: npm run test       Result: PASS/FAIL/NOT RUN
Command: npm run lint       Result: PASS/FAIL/NOT RUN
Command: npm run build      Result: PASS/FAIL/NOT RUN
Tenant isolation tests      Result: PASS/FAIL/NOT RUN
Manual scenario             Result: PASS/FAIL/NOT RUN
```

Never claim the application is secure or production-ready only because generated code compiles. Block real client onboarding until critical controls have been tested and reviewed.
