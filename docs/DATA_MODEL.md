# Data Model and Invariants

**Status:** Proposed logical schema. Actual tables, SQL types, policies and migration filenames must be defined/verified during M1 and recorded in `PROJECT_STATE.md`.

## Core entities

| Entity | Required ownership / relationships | Key concepts |
| --- | --- | --- |
| `organizations` | Global organisation ID | Name, timezone, state, plan context |
| `organization_members` | `organization_id`, `user_id` | Role, join/revoke dates; uniqueness |
| `customers` | `organization_id` | Contact fields, archival status |
| `service_addresses` | `organization_id`, `customer_id` | Site address, access notes |
| `equipment` | `organization_id`, `service_address_id` | Manufacturer, model, serial, install date |
| `jobs` | `organization_id`, `customer_id`, `equipment_id?`, `assigned_to?` | Scheduled time, status, details |
| `job_reports` | `organization_id`, `job_id`, `technician_id` | Checks, notes, completion time |
| `maintenance_plans` | `organization_id`, `equipment_id` | Schedule/interval, next due date |
| `attachments` | `organization_id`, `job_id?`, `object_key` | Private storage metadata |
| `notification_deliveries` | `organization_id`, related record | Channel, dedupe key, delivery status |
| `quotes`, `quote_items` | `organization_id` | Draft/service quote data; later milestone |
| `subscriptions` | `organization_id` | Stripe IDs, verified status, plan |
| `integration_connections` | `organization_id` | Provider metadata; tokens stored as secrets |
| `external_mappings` | `organization_id`, provider, entity type | External ID to internal ID mapping |
| `import_jobs`, `audit_events` | `organization_id` | Batch processing and history |

## Isolation invariants

1. Every tenant-owned row includes an immutable `organization_id` enforced by RLS and authorisation.
2. Cross-tenant foreign references must be impossible: use tenant-matched composite FK or equivalent validated relational constraint, not just a filtered UI dropdown.
3. Unique identifiers that are external/customer-visible are scoped appropriately (e.g. `(organization_id, external_provider, external_id)`).
4. User account identity is global; organisation membership can be many-to-many. Active context must be checked per operation.
5. Tenant-owned files are private and access-controlled by associated database records and storage policies.
6. Prefer soft archival for customer/business records with service history. Define erasure rules with `PRIVACY.md`.
7. Timestamps stored unambiguously in UTC, with organisation timezone for display and recurrence rules.

## Relationship sketch

```text
organization -> members
organization -> customers -> service_addresses -> equipment -> maintenance_plans
organization -> jobs -> job_reports
                  |-> attachments
                  |-> notification_deliveries
organization -> subscriptions
organization -> integration_connections -> external_mappings
```

## Migration standards

- SQL migrations are committed and applied first to development, then staging, then production with review.
- Policy migration changes need positive + negative RLS tests.
- Destructive migrations require backup, rollback strategy, client-impact review and human approval.
- Don't assert an ERD or table exists unless its migration is present and applied.
