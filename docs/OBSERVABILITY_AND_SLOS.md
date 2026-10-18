# Observability, Support and Pilot Reliability

## Monitor the following

Request error rates (4xx vs 5xx), p95 HTTP latency, DB connection saturation, failed migrations, auth failures, unauthorised access denials, storage errors, failed import rows, long-running jobs, email failure/retries, background queue age if enabled, storage usage/cost.

## Log schema

`timestamp, environment, service, route, request_id, actor_id (pseudonymous), organization_id (opaque), resource_type/id, outcome, duration_ms, error_code`. Sanitise query and request bodies; never log passwords, access tokens, customer addresses, private photo URLs or uploaded CSV rows.

## Pilot targets — to be agreed, not guarantees

Initial smoke expectations: critical page loads on normal office/mobile network; dashboard queries bound by pagination/date ranges; import failure visible; 500s alert operator; no data loss on retry. Choose uptime, latency, storage volume, backup RPO/RTO and response SLAs with real client before contractual commitments.

## Incident response

Severity P0: suspected data exposure/loss → suspend risky operations, notify designated privacy/security lead, preserve evidence, assess notification requirements. P1: main booking/report flow down → rollback/forward-fix with incident note. Other issues triaged by impact. All incidents have owner, timeline and root-cause follow-up.

## Operational ownership

Founder is first responder until a support rota exists. Client owner is notified of planned maintenance. Confirm what counts as included maintenance versus billable features. Require explicit client permission for production support data access.
