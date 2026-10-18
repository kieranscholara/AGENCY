# Product Brief — AC Service Manager

**Status:** Proposed product requirements; no client discovery or implementation is implied.

## Customer and value proposition

Target: small-to-medium AC installation, repair, and maintenance firms, initially in Malta and potentially other markets. Help office staff manage bookings and equipment histories and help technicians complete jobs in the field. Encourage repeat service through accurate, permissioned reminders.

**Positioning:** AC-specific service operations, not a general ERP.

## Personas

| Role | Goal | Initial scope |
| --- | --- | --- |
| Business owner | See work, users, service obligations, subscription | Full company admin |
| Office manager | Schedule visits and manage records | Jobs, customers, quotes, equipment |
| Technician | View assignments and submit evidence | Assigned jobs, reports, approved uploads |
| Platform operator | Maintain healthy subscription service | Tenant status, usage, operational diagnostics; no blanket private-data access |

## MVP (ordered by business value)

1. Secure accounts, business membership, and role-based access.
2. Customer/contact and service-address records.
3. Installed AC equipment with serial/model and service history.
4. Calendar/list of jobs, assignment, and state transitions.
5. Mobile-usable technician checklist, notes and job photographs.
6. Service report and next-due calculation with opt-in/approved reminders.
7. Exportable record or PDF service report.
8. Guided CSV customer/equipment import for onboarding.
9. SaaS billing and basic plan enforcement before self-service commercial rollout.

## Explicitly out of MVP

AI features, full ERP/invoicing, purchasing, route optimisation, native mobile applications, consumer login, unsupervised messaging, complicated two-way integrations, and a custom visual workflow builder. Re-evaluate only after real client demand.

## Commercial assumptions — NOT validated

- Candidate monthly packages approximately €49/€99/€199; test willingness to pay rather than treating these as established prices.
- Initial pilot: ideally two to three small businesses, with explicit terms and feedback.
- Success is real usage, retained customers, fewer missed visits or reduced admin, not merely an attractive dashboard.

## Unknowns

See `OPEN_QUESTIONS.md`. Finalise the product workflow after interviewing at least several target companies. Record validated decisions in `DECISIONS.md`.
