# External System Integration Architecture

**First client unknown.** No provider can be promised until its API/licensing/authorised access are verified. Pilot default = secure CSV import, not custom two-way integration.

## Connector layers

```text
Tenant/company integration settings
    -> connection service (authorisation, token life cycle)
    -> provider adapter (provider API and webhooks)
    -> mapper (provider schema <-> canonical domain)
    -> sync processor (paging, deltas, retries, idempotency)
    -> application service (tenant validation, DB constraints)
    -> reconciliation report and monitoring
```

## Required connection record

`organization_id`, provider type/connection ID, authorising owner, scopes, state (`pending/connected/reconnect_required/disabled`), last successful sync, last error summary and token reference to secure storage. Never store raw provider secret in project Markdown, React state or audit log.

## Data authority matrix (pilot assumptions)

| Entity | Default owner | Sync allowed? |
| --- | --- | --- |
| Service visit and checklist | AC Service Manager | Outbound later |
| Contacts | Decide with client | Import first; inbound later |
| AC equipment/unit | AC Service Manager | Import first |
| Accounting invoices and VAT | Existing accounting platform | Do not duplicate accounting authority |
| Staff list | AC Service Manager / authorised identity source | Inbound only after approval |

## External record mapping

Unique constraint on `(organization_id, provider, external_object_type, external_id)`; track internal object ID, provider version/etag, mapped timestamp and source lastModified. Use stable primary IDs rather than fuzzy matching once linked.

## Synchronisation lifecycle

1. Connection handshake with client-authorised provider account, least privileges, test credentials.
2. Full backfill in batches with pagination and mapping preview; counts and sample reconciliation.
3. Incremental sync via provider supported webhooks or cursor/timestamp. Webhook signature verifies raw payload, replay checked by event ID.
4. Worker handles idempotent upsert and bounded retries (429 uses Retry-After; transient 5xx backoff).
5. Reconciliation checks record counts, missing records, changed conflicts; provide operator alert/dashboard.
6. Disconnect revokes token where provider permits, stops jobs, exports/maps/retains data per contract.

## Two-way sync stop rule

Do not turn on bidirectional contact edits until each field has a source-of-truth conflict rule, concurrency/version checks, overwrite prevention and human-readable rollback/reconciliation procedure.

## Failure matrix

| Failure | Response |
| --- | --- |
| Token expired/revoked | Mark reconnect required, notify authorised admin; don't retry endlessly |
| Rate limited | Exponential backoff + Retry-After, cap concurrent requests |
| Network/timeouts | Retry idempotent calls only, reconcile before reissuing non-idempotent writes |
| Invalid record | Quarantine with redacted reason; continue safe records if batch design permits |
| Webhook replay/out-of-order | Store event ID, fetch authoritative provider state when required |
| Cross-tenant mapping mismatch | Reject, alert, do not mutate records |
| Provider API unavailable | Keep local workflow usable, queue/inform only if required |

## Integration discovery card for first client

Product/vendor, exact version/plan, API docs, permitted scopes, data entity list, direction, volume, sync freshness SLA, test account, responsible client admin, legal/privacy review and estimated dev/testing time. Without these, integrations remain **out of scope** for the pilot.
