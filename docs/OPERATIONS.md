# Running the SaaS: Support, Reliability and Recovery

## Monitoring targets

- App errors and latency, failed authentication patterns.
- Database query performance, pool and capacity.
- Background job failures, oldest queued task, duplicates.
- Email delivery failures, bounce/opt-out compliance.
- Integration token expiry and failed syncs.
- File storage growth, errors and costs.
- Stripe event processing and subscription reconciliation.

No uptime SLA is promised yet. Measure actual service before setting a contractual SLA.

## Operator dashboard

See organisation status, plan, user count, import/sync failures, task health and aggregate usage. Avoid granting routine support staff unrestricted access to private customer records. Exceptional access requires permission, purpose, limited duration and audit.

## Support workflow

1. Client submits issue and reproduction steps.
2. Categorise: security/privacy, outage, blocking workflow, or general request.
3. Check logs/telemetry with request IDs but no sensitive payloads.
4. Reproduce with synthetic data on staging.
5. Fix in branch, verify, obtain review and release.
6. Notify affected client where appropriate; record cause and preventive test.

## Backups and recovery

- PostgreSQL scheduled backups and documented restore process.
- Separate plan for Supabase Storage file contents; DB backups alone do not restore uploaded photos/files.
- Retain migrations and deployment artifacts.
- Perform restore drills in isolated environment before launch and periodically afterward.
- Define recovery point/time objectives after assessing clients' requirements.

## Security incidents

Restrict/rotate affected credentials, preserve evidence, assess scope, follow contract/GDPR obligations and seek qualified advice for notification requirements. Record timeline, corrective action and tests that prevent recurrence.

## Cost controls

Track per-tenant storage, active users, jobs, email volume, sync frequency, support time and infrastructure spend. Set alerts before usage surprises. Plan upgrades based on measured workload, not arbitrary customer-count thresholds.
