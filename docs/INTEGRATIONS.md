# External Integration Strategy

## Guiding rule

First learn what a client currently uses. Most first customers should onboard through validated CSV/Excel import. Only build a provider connector after a concrete business use case and authorisation exist.

## Priority sequence

1. Manual entry for small data sets.
2. CSV import/export with dry-run preview and reconciliation.
3. Read-only provider API integration for verified high-value workflow.
4. Controlled outbound sync and webhooks where operationally necessary.
5. Two-way sync only with explicit source-of-truth/conflict rules.

## Provider connector contract

Each connector defines supported provider/version, scopes, authentication, canonical entity mapping, stable external IDs, pagination, delta-sync strategy, rate-limit behaviour, retries, idempotency, failure visibility, and account disconnect.

Store `(organization_id, provider, external_entity_type, external_id)` to map external records to internal IDs. Never assume an external ID is unique across tenants or providers.

## Data ownership examples

| Data | Proposed authoritative system | Note |
| --- | --- | --- |
| AC unit service report | AC Service Manager | Completed here |
| General ledger/invoices | Existing accounting app | Do not mirror as finance authority |
| Contact phone/email | Decide per connection | Prevent conflicting writes |
| Job schedule | AC Service Manager | Unless client has master field-service tool |

## CSV import checklist

Client authorises transfer; upload to private temporary location; parse without executing spreadsheet formulas; map columns; validate dates/phones; detect duplicates; dry-run preview; explicit client confirmation; idempotent commit; audit and reconciliation report; deletion/retention of source file.

## Integration security

Use provider-supported OAuth where appropriate, least scopes, state validation, encrypted tokens, key rotation, signature-verified webhooks and bounded retries. Never send credentials to coding agents or store them in Markdown.

## Failure behaviour

Log provider error code safely, mark connection unhealthy, retry only recoverable errors, cap retry count, provide reconnection flow, and reconcile missed webhook events through periodic sync where needed. Never silently delete or overwrite client records on provider failures.

## Provider decisions

**No specific CRM/accounting/POS connector has been approved yet.** Record client systems, licensing and availability in `OPEN_QUESTIONS.md` after interviews.
