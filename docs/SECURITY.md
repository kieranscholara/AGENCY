# Security and Multi-Tenancy Contract

**Priority:** Blocking for any real customer data. This is a specification, not a certification.

## Trust boundaries

- Browser is untrusted. All request IDs, roles, organisation IDs, file keys and price/plan claims can be tampered with.
- Verify sessions on the server; verify membership/role for the specific organisation and action.
- Use user-scoped Supabase/database access so RLS applies to tenant operations. Do not use a bypass-RLS admin key in ordinary user handlers.
- Authorisation runs on reads, writes, updates, deletions, nested references, exports and file downloads.

## Role policy (draft — validate with pilots)

| Action | Owner | Manager | Technician |
| --- | --- | --- | --- |
| Change subscription/company settings | Yes | No | No |
| Invite/revoke staff | Yes | TBD | No |
| Manage customers/equipment | Yes | Yes | Read limited to assigned work |
| Schedule/assign jobs | Yes | Yes | No |
| Read jobs | Company-wide | Company-wide | Assigned/otherwise explicitly allowed |
| Submit job report | Yes | Yes | Assigned jobs only |
| Read private photos | Authorised | Authorised | Assigned jobs only |

Platform support/admin uses independent privileged access with deliberate approval and audit; ordinary operators should see health/usage without browsing sensitive customer data.

## Database RLS checks

- Enable policies for **every** exposed tenant table; use least-privilege grants.
- Check active membership before granting tenant access.
- Apply `USING` and `WITH CHECK` consistently to block cross-tenant inserts/updates.
- Reject cross-tenant foreign-key references even if a user guesses UUIDs.
- Test user with no membership, revoked member, dual-tenant member, technician, manager and owner.
- Do not trust JWT role metadata editable by users; sensitive roles require trusted storage.

## Files

Private Supabase Storage buckets; random server-generated object keys; MIME/type and size limits; signed URLs with short expiry or authenticated access; inspect or scan uploads where risk warrants; image metadata hygiene; prevent cross-org reads even when URL/key is guessed.

## External boundaries

- Store provider credentials server-side using managed secrets/encryption. Restrict OAuth scopes; support revoke/disconnect.
- Verify Stripe and provider webhook signatures before parsing/trusting actions.
- Use idempotency records to prevent duplicate imports, charges or messages.
- Rate-limit login-sensitive and expensive endpoints; anti-abuse protections for invites/uploads.

## Incident preparation

Audit privileged actions and account changes without logging customer secrets. Document credential rotation, compromised account lockout, recovery of backups, incident reporting and client communication in `OPERATIONS.md`.

## Mandatory pre-pilot checks

- Two-tenant API/RLS/storage isolation suite passed.
- Reviewed client onboarding and membership escalation tests.
- No secrets in repo, runtime logs, client bundle or agent context.
- Backup and storage recovery plan tested.
- Human security review of tenancy and auth before onboarding client data.
