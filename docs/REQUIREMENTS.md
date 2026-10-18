# Functional Requirements and Acceptance Criteria

**Status:** Proposed. Each acceptance scenario must be converted into automated and/or documented manual tests. Avoid silently expanding scope.

## M1 — Secure company accounts

- A verified user may join an organisation only through an approved signup/invitation process.
- Only a permitted owner can invite, revoke, or change organisation members.
- Staff roles: `owner`, `manager`, `technician`. A platform operator is a **separate**, privileged identity/claim, not simply another tenant role.
- Requests for another organisation's records return no private data, whether an attacker changes a URL, body, query, JWT context, or file path.
- A user belonging to two organisations must select context; server independently validates membership for each operation.
- Account suspension and membership removal take effect on subsequent authorised requests.

**Acceptance:** Two independent organisations with separate users, fixtures and attachments. Cross-company read, write, list, update, delete, and download attempts all fail. Privilege escalation attempts fail.

## M2 — Customer and equipment

- Staff with permission can create/search/edit their company's customers.
- Customer may have multiple service addresses; address may contain multiple AC units.
- AC unit includes manufacturer, model, optional serial, installation date if known, and service history.
- Deleting a customer with active jobs uses deliberate archival/retention rules; no accidental cascade deleting service history.

**Acceptance:** Company A cannot reference Company B's address or equipment ID when creating a record.

## M3 — Jobs and scheduling

- Manager schedules a visit in local business time, stored unambiguously (UTC + time zone where required).
- Job has status `scheduled → assigned → in_progress → completed` or `cancelled`; supported rescheduling and reassigning must be audited.
- Assigned technician sees only jobs allowed by role policy; completion produces a durable timestamp and immutable-enough audit trail.
- Avoid silent double booking. Initially warn/confirm conflicts; define blocking rules with pilot customers.

**Acceptance:** Repeating a request must not create duplicate jobs or notifications when idempotency is specified.

## M4 — Field reporting

- Technician completes structured checklist with notes, service date, and authorised photo attachments.
- Private customer photos are accessible only to authorised company staff.
- Generated report includes correct customer, equipment, technician and visit metadata.

## M5 — Maintenance reminders

- Due date is calculated from an explicit business-defined interval, not fabricated by AI.
- Do not send messages without appropriate contact basis/preferences and an approved delivery schedule.
- Retry failures safely; duplicate dispatch is prevented by a unique reminder/delivery key.

## M6 — Operational/commercial readiness

- Tenant onboarding, CSV preview and validation, subscription billing, support process, monitoring, backup + restore test, staging, and deployment approvals.
- Usage limits and suspended billing states must be enforced on the server.

## Non-functional requirements

- Responsive, keyboard-friendly web UI; mobile technician workflow works on common phone widths.
- Service and API errors do not leak secrets or cross-tenant details.
- Automated checks cover auth, isolation, data constraints, uploads, and billing/webhooks when those modules exist.
- Performance budgets and uptime objectives remain **TBD**, to be measured during pilot.
