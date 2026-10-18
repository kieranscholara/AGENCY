# Authn / Authz / Tenant Access Matrix — Pilot

**Requires client approval before implementation.** `platform_admin` is separate trusted operator privilege, not a role the user can self-assign or edit. Company staff belong via `organization_members` rows and may belong to more than one organisation.

| Action | Owner | Manager | Technician | Platform operator |
| --- | --- | --- | --- | --- |
| View company settings | Yes | Yes | Read basic only | Operational metadata only |
| Invite/revoke staff | Yes | No (pilot) | No | Via audited break-glass only |
| View/search customers | Yes | Yes | Only customers on assigned jobs, if required | No default access |
| Create/update customer | Yes | Yes | No | No default access |
| Create equipment/address | Yes | Yes | No | No default access |
| View jobs | All company jobs | All company jobs | Assigned jobs only | Metadata by default |
| Create/assign/reschedule jobs | Yes | Yes | No | No default access |
| Start or complete job | Yes | Yes | Assigned job only | No default access |
| Attach photos to job | Yes | Yes | Assigned job only | No default access |
| Download job photos | Yes | Yes | Assigned job only | No default access |
| Preview and commit imports | Yes | Yes, if enabled | No | No default access |
| Billing and subscription | Yes | No | No | Metadata/support only |
| Edit global platform config | No | No | No | Yes, separately authorised |

## Permission implementation rule

- Resolve caller identity from verified server auth, active organisation and membership, then evaluate operation and resource-specific permissions. Frontend hiding does not constitute authorisation.
- Database policies prevent organisation cross-read/write, including file metadata. Service/API layer additionally limits technicians to **assigned jobs** and associated customer/equipment/photo access. Ideally enforce sensitive assignment restrictions at DB RLS as well if end users can query exposed tables directly.
- Reassignment revokes prior technician access on next request; revocation of membership invalidates access without waiting for app cache expiry.
- All related IDs on jobs (customer, address, unit, technician) belong to same company and satisfy relationships.
- Avoid recursive RLS policy dependency on membership table. Implement and test membership helper functions and grants safely with qualified review.

## Mandatory negative tests

1. Org A owner reads/updates/creates references to Org B's resources — denied, no private leakage.
2. Org A employee guesses Org B private attachment path — denied.
3. Org A technician views another company's records — denied.
4. Technician views same-company **unassigned** job/customer/photo — denied under approved policy.
5. Technician attempts self-promote or invite staff — denied.
6. Revoked member retains stale session but accesses any company data — denied.
7. Cross-org foreign-key values on new job — rejected by relational constraint.
8. User belongs to two orgs, switches selected context, old company IDs submitted — server checks context and denies.
9. Privileged service-role use is absent from client and audited for server jobs.

## Admin support access

No direct browsing of subscriber customer databases through normal platform-admin UI. If needed, require documented customer authorisation, time-limited access, purpose limitation and audit event. Never give coding agents permanent superuser access.
