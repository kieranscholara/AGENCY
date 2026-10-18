# Frontend ↔ Backend Contract

**Status: proposed.** Standard flow is server-rendered initial reads and typed client mutations via JSON endpoints, with domain services shared between reads and writes. Do not invent a second mutable client-side business authority.

## UI pages and data ownership

| UI | Server read | Browser mutation | Error/loading behaviour |
| --- | --- | --- | --- |
| Login | Current verified user | Auth SDK/login callback | Invalid credentials; expired invite |
| Customers | Page/search scoped by org | `POST/PATCH /api/v1/customers` | 400 validation, 404 hidden cross-tenant ID, duplicate conflict |
| Customer detail | Customer with addresses/equipment | Add equipment/address | Missing membership, archived customer |
| Jobs calendar | Bounded date range for permitted jobs | Job scheduling and assignment | 409 overlap/version conflict |
| Technician job | Assigned or permitted job | Start/complete/report | 403 not assigned, 409 already completed |
| File attachments | Metadata + authorised download grants | Upload grant + finalise | Upload expired, invalid file, storage failure |
| Imports | Staging job/preview counts | Upload, preview, confirm | Validation/reconciliation failures |

## Typed fetch convention

- Browser sends `Content-Type: application/json`, session cookie as appropriate, `X-Request-ID` optional, `Idempotency-Key` for retriable creates/complete flows.
- API authenticates by trusted server mechanism; selected organisation resolved/checked against membership; inputs parsed with Zod; no massive unbounded body.
- Successful create returns 201 + resource object. Update 200 + updated version. Delete/archive 200/204 as contract defines.
- Error envelope `{ "error": { "code": "VALIDATION_ERROR", "message": "Check the submitted fields", "requestId": "...", "fields": { "name": "Required" } } }` (fields optional). Never leak existence of another tenant's record.
- UI avoids optimistic updates for irreversible state changes; on conflict refetch and show resolution message.
- Use ETags or `version` for conflicting updates; do not rely on "last form submit wins" for schedules.

## Session/security assumptions to verify in actual repo

Cookie-based web auth plus CSRF/origin protection where relevant; avoid exposing privileged tokens to browsers. Server Components may use authenticated server Supabase client with RLS, but a service-role DB client **bypasses** RLS; privileged work must be isolated, audited and explicitly tenant-scoped.

## Dates

Input includes offset (e.g. `2026-11-10T09:00:00+01:00`) and organisation IANA time zone; store UTC instants; display using selected organisation zone. For recurrent jobs, store local clock + IANA zone + recurrence rule; handle DST explicitly. For Malta `Europe/Malta` is typical, but do not force if serving others.

## Accessibility and mobile

Keyboard form errors linked to inputs; visible success/failure; max-width layouts for technician phone; no assumption of offline operation, which is **deferred** unless client requires it.
