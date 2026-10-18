# Asynchronous Jobs and Reminders

**Pilot scope default:** No automatic outbound reminders; user can see upcoming due dates and trigger manual follow-up. If a client contract requires reminders at go-live, enable this module only after consent/legal basis, reliable dispatch and duplicate-delivery tests.

## Message categories

Staff invitation (transactional); completed service report (if client chooses); due service reminder (client-controlled); marketing (out of scope, separate legal basis/consent).

## Scheduling

Store maintenance plan with schedule in company time zone and next due date. A daily worker selects eligible records based on rules, contact preferences and company configuration. It creates unique delivery intents rather than sending directly during report completion.

## Durable execution

Commit event intent to `outbox_events` with business transaction, e.g. `service_report.completed.v1`. Worker dequeues and creates `notification_deliveries` using unique `(organization_id,rule_id,equipment_id,due_date,recipient)` dedupe. Send via Resend, store provider message ID and retryable status. A task may execute twice and must have idempotent effects. Where provider can't guarantee exactly-once delivery, avoid claiming perfect deduplication.

## Failure classification

Permanent invalid recipient / opt-out → don't retry; network / 5xx → bounded retry with jitter; quota/billing/401 → pause and alert; unknown provider response → reconcile before resending where possible. Produce operator dashboard and audit.

## Tests

Fake clock around Europe/Malta DST boundaries, replay of job complete, same due reminder scanned twice, retry after send-time timeout, opt-out, revoked org, paused subscription, tenant isolation, idempotency unique constraints. Avoid scheduling one in-memory timer per equipment.
