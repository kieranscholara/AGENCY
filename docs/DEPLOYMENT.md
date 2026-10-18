# CI/CD, Staging and Production Releases

## Source control policy

- Work in a feature branch with a clear issue or milestone.
- Open a pull request with test evidence, screenshots where relevant, and a migration checklist.
- Require review before merge, including human approval for auth/tenant/billing/security changes.
- Branch protection and required CI checks should be enabled before a pilot launch.

## Suggested promotion flow

```text
Local changes + tests
      ↓
Feature branch / pull request
      ↓
CI checks + review
      ↓
Preview environment with non-production data
      ↓
Merge to main → Staging deploy + migration
      ↓
Staging E2E / client acceptance
      ↓
Explicit human approval
      ↓
Production backup/rollback checkpoint
      ↓
Production migration + deploy
      ↓
Smoke tests + monitoring
```

## Database releases

Use ordered version-controlled migrations. Run on staging first and confirm constraints, policies and indexes. For destructive changes, plan additive/backfill/cleanup stages, downtime impact and rollback/data recovery. A code rollback may not undo a destructive migration.

## Release checklist

- [ ] Scope and acceptance criteria confirmed
- [ ] Secrets and permissions reviewed
- [ ] Automated tests + build passed
- [ ] Cross-tenant regression tests passed for relevant changes
- [ ] Database migration reviewed and staged
- [ ] Relevant client approval recorded
- [ ] Backup/restore plan checked
- [ ] Production deploy explicitly approved
- [ ] Smoke tests succeeded
- [ ] Monitoring checked after deploy
- [ ] Release notes / project state updated

## Incident rollback

If errors rise or critical workflow fails: stop rollout, disable new feature if safely possible, revert application release, evaluate data migration separately, communicate impact, and record postmortem in `OPERATIONS.md`.

Actual Vercel/Supabase/CI configuration has not yet been verified.
