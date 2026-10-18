# Pilot Acceptance & Go/No-Go Checklist

**Stop if any critical security, data loss or recovery item is FAIL/NOT TESTED.** Record commit, environment, reviewer, date and actual evidence; don't mark as PASS because an agent asserted it.

## Security and isolation (critical)

- [ ] Owner A cannot list/view/update/delete customer/job/attachments of Owner B.
- [ ] Technician cannot see another company's resources or unassigned same-company jobs/photos.
- [ ] Unauthenticated and revoked users cannot access protected endpoints; role elevation denied.
- [ ] Cross-org references (customer/address/equipment/technician) rejected by DB constraints.
- [ ] No public photo buckets, no privileged keys in bundle or git; secret scan clean.
- [ ] API input validation, rate limits for sensitive actions, secure authentication and CSRF/origin protection checked.

## Core workflow (critical)

- [ ] Two company owners independently log in and manage their own records.
- [ ] Owner adds customer, address, AC unit and schedules job.
- [ ] Assigned technician uses phone to view/start/complete service job; incorrect status transition denied.
- [ ] Completion creates durable report, service history and audit event; retry doesn't duplicate.
- [ ] Stale concurrent job edit gives understandable conflict instead of silent overwrite.
- [ ] App remains usable on target phone and browser; errors are understandable.

## Data and integration (critical if in scope)

- [ ] Migration preview validated and signed; total rows created/updated/skipped/errors reconciled.
- [ ] Company source data and export permission documented; production data handled per DPA.
- [ ] Third-party integration tested with real provider sandbox/account and failure modes; omit from pilot if not verified.
- [ ] Photo/PDF upload restricted by MIME/size, job permission and private storage policies, with actual download denial tests.

## Production operation (critical)

- [ ] CI lint, typecheck, build, relevant tests and schema checks PASS at tagged release commit.
- [ ] Staging/prod segregated; migrations run on staging then production with reviewed plan.
- [ ] Error monitoring and request tracing working; incident contact and support channel known.
- [ ] Database **and stored file** recovery tested in isolated environment; restore evidence recorded.
- [ ] Reviewed deploy/rollback plan, smoke test and critical incident escalation ready.
- [ ] Access and privacy contracts, retention, client signoff and risk disclosures recorded.

## Client UAT examples

1. "Schedule a visit for Unit X at Address Y, assign it to Staff Z, view on Staff Z's phone, complete it and open history."
2. "Create a second company and attempt to view the first company's records and images; confirm denied."
3. "Import 20 agreed examples; reconcile customer, AC unit and dates and explain every skipped row."

## Release decision

Release name / commit / date / approver:
PASS/FAIL/NOT RUN per checklist:
Unresolved critical blockers:
Decision: **GO / NO GO**
Client signoff reference:
