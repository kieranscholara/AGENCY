# Restricted Production Pilot — Release and Recovery Runbook

**Status: template, not an executed runbook.** Named release manager: TBD. Production and staging access: TBD. Do not release until client accepts scope and tests.

## T-5 business days

1. Freeze launch must-haves and identify deferred features with client.
2. Confirm privacy/DPA/terms, domain/email, incident/support contacts and production access owners.
3. Record exact release commit SHA, migration list, dependencies, known defects and monitoring.
4. Verify schema/tenant test results, staging UAT and private upload rules.
5. Test DB restore **and** object-storage file recovery on isolated environment; record time, results and gaps.

## T-1 day

- Create reviewed deployment/checklist PR; verify no secrets in repo; reviewer signs auth/tenant/data changes.
- Verify backup schedule and current successful backup, retention and storage snapshots/replication mechanism.
- Decide if data cutover requires write freeze on old system; agree backup and final delta plan.
- Ensure app deployment artifact known and prior version rollback possible. Additive/compatible migrations only for short rollback window.

## Launch sequence

1. Run schema migrations against production using approved human operator and record success.
2. Deploy tagged app build, confirm HTTPS/login/domain/auth callback.
3. Exercise smoke flow: company owner logs in → creates customer/unit/job → technician completes job → owner views history.
4. Exercise negative tenant test against **synthetic fixtures**, not real clients.
5. If included, upload/authorise/download one test photo; import the final signed-off dataset and reconcile.
6. Check Sentry/logs and DB performance; enable only approved outbound messaging.
7. Pilot limited users; daily monitoring for first week.

## If something fails

- Security/data leak: stop affected feature, revoke compromised access, preserve evidence and escalate; follow privacy/contract requirements.
- Bad app release: rollback deployment to previously working build **only if schema is compatible**.
- Schema change failure: use reviewed forward-fix or tested reversible migration; don't blindly delete columns or revert production data.
- Bad import: stop job, preserve reconciliation artifacts and follow batch-level recovery plan with client approval.
- Provider outage: degrade gracefully, defer async work and alert affected users.

## Post-launch

Document release, actual incident responses, open defects and client support channel. Schedule UAT follow-up and define when pilot can expand beyond restricted staff.
