# PostgreSQL Implementation Blueprint — Proposed, Needs Migration Review

These are implementation **requirements and SQL sketches**, not ready-to-run migrations. Verify real auth schema, Supabase SDK/version and existing migrations. Have a senior engineer independently review RLS/privileged functions before live data.

## First-launch tables

`organizations`, `organization_members`, `customers`, `service_addresses`, `equipment`, `jobs`, `job_reports`, `attachments`, `audit_events`, `import_batches`, `import_rows` (if CSV import is in scope). Defer Stripe, quotations, external connector tokens, reminders and advanced recurrence to later milestones unless signed pilot needs them.

## Key invariant: composite tenant FKs

Use UUID PKs and `organization_id uuid not null` for every tenant-owned row. On referenced tenant-owned tables add unique index/constraint on `(organization_id,id)`; define referencing relation as `(organization_id,customer_id)` → `customers(organization_id,id)` etc. This makes it impossible for an Org A job to reference an Org B customer even when backend has a bug.

Example **partial pattern**, adapt in reviewed migration:

```sql
-- Illustrative, not a complete standalone migration.
ALTER TABLE public.customers
  ADD CONSTRAINT customers_org_id_id_unique
  UNIQUE (organization_id, id);

ALTER TABLE public.jobs
  ADD CONSTRAINT jobs_customer_same_org_fk
  FOREIGN KEY (organization_id, customer_id)
  REFERENCES public.customers (organization_id, id);
```

Apply analogous constraints for service addresses→customer, equipment→service address, jobs→equipment/address, reports→job, attachments→job. A separate validated membership FK/role constraint must cover assignment.

## RLS policy policy (not full SQL)

- Enable and **force** RLS on tenant tables as appropriate; revoke broad public grants. Grant authenticated client only minimum necessary operations.
- SELECT and mutation USING/WITH CHECK evaluate actor active membership and appropriate job assignment/role, not merely equality with any user-supplied org ID.
- For complex privilege checks, use narrowly defined reviewed `SECURITY DEFINER` helper with locked-down `search_path`, explicit qualified table names and safe grants; avoid recursive policy checks.
- Service-role bypass is expected: server-only jobs need explicit application-level tenant verification and audit.
- Explicitly deny anonymous access where inappropriate; client cannot create platform admin roles or membership by direct table insert.

## Concurrency

On jobs add `version integer not null default 1`, update via transaction with `WHERE version = expectedVersion`; 0 rows → 409 conflict. Prevent duplicate service completion with unique active report or explicit revision relation. If multiple jobs may overlap, define whether conflict is warning or hard block and test races.

## Migration structure

`supabase/migrations/<timestamp>_org_members.sql`, ...; review separate RLS migration, then tests. Never mutate already-applied prod migration history. Staging migration test must include two organisations, two owner accounts and technician, and intentionally invalid cross-org foreign references.

## Indexes and lifecycle

Index `(organization_id, customer_id)`, `(organization_id, scheduled_at)`, `(organization_id, assigned_to, scheduled_at)`, `(organization_id, status)` as query warrants. Paged list endpoint default limit 20/max100. Use archival/retention policies rather than cascaded deletion of signed-off service history. Validate performance based on real fixture sizes.
