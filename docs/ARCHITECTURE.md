# HTTP API Contracts (Proposed v1)

These are **target routes**, not implementation claims. Keep controllers thin and reuse server services. Where Next.js Server Components can read server-side directly, avoid duplicate browser fetches; retain explicit APIs where useful for integrations and interactive actions.

## General contract

- Base path: `/api/v1` (unless actual framework architecture changes by approved ADR).
- Auth: secure cookie-backed authenticated session; server revalidates identity and membership.
- Tenant: selected organisation must be validated against membership. Do **not** trust user-provided `organizationId` as authority.
- Request validation: Zod or equivalent runtime schema.
- Identifiers: UUID or consistently validated opaque IDs.
- Time: ISO 8601 with offset on input, UTC in storage.
- Pagination: `limit` with maximum + opaque cursor for lists.
- Errors: no internal traces or other-tenant data.

## Suggested response conventions

Success: documented resource JSON. Error: `{ "error": { "code": "VALIDATION_ERROR", "message": "...", "requestId": "..." } }`.

Recommended status codes: `400` invalid input, `401` unauthenticated, `403` unauthorised, `404` not found (including concealed cross-tenant resources), `409` conflict, `422` domain rule violation, `429` limited, `5xx` internal.

## Initial endpoints

| Method + path | Responsibility | Minimum authorisation |
| --- | --- | --- |
| `GET /organizations/current` | Company settings | Member |
| `GET /members` | Members of current company | Owner/manager per policy |
| `POST /members/invitations` | Issue scoped invitation | Owner |
| `GET /customers` | Paginated customer search | Owner/manager |
| `POST /customers` | Create customer | Owner/manager |
| `GET /customers/:id` | View customer | Role-scoped |
| `PATCH /customers/:id` | Update customer | Owner/manager |
| `POST /service-addresses` | Register site | Owner/manager |
| `POST /equipment` | Register unit | Owner/manager |
| `GET /jobs` | Filtered jobs | Role-scoped |
| `POST /jobs` | Schedule visit | Owner/manager |
| `PATCH /jobs/:id` | Update assignment/status | Role + transition rules |
| `POST /jobs/:id/report` | Submit report | Assigned technician or permitted manager |
| `POST /attachments/upload-grant` | Grant upload for authorised job | Job scope |
| `POST /imports/preview` | Preview CSV mapping | Owner/manager |
| `POST /imports/commit` | Confirm validated import | Owner/manager |
| `POST /billing/checkout` | Initiate hosted Stripe checkout | Owner |
| `POST /webhooks/stripe` | Receive signed webhook | Verified provider signature |

## Example: schedule a job

```json
{
  "customerId": "<uuid>",
  "serviceAddressId": "<uuid>",
  "equipmentId": "<uuid>",
  "technicianId": "<uuid>",
  "scheduledAt": "2026-11-10T09:00:00+01:00",
  "jobType": "routine_service"
}
```

Server must verify that all referenced records belong to the same organisation and that the technician has a valid membership. Do not directly insert an entire user-provided object into the DB.

## Versioning and testing

Breaking changes require migration/version policy. For each endpoint include success, unauthenticated, forbidden, invalid input, cross-tenant, and relevant concurrency/retry tests. Add OpenAPI schema when endpoints are stable and external consumers exist.
