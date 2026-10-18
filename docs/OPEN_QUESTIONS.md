# Open Questions — Human Decisions Needed

Do **not** invent answers. Work may proceed on independent low-risk tasks, but stop before a decision that depends on an unresolved item.

## Immediate setup (answer before implementation)

1. **Repository starting point:** Is this an actual Next.js + Supabase starter, a Lovable-generated React application, or a different existing codebase? (Affects all framework instructions.)
2. **Agency ownership:** What GitHub organisation should own the product, and what should the product be called in the UI? (`AC Service Manager` is a working name.)
3. **First pilot market:** Only Malta initially? Which business language, business timezone and appointment conventions should be supported?
4. **Authentication:** Email/password, magic link, or both? Will companies use staff invitations initially?
5. **Pilot approach:** Are we building a demonstration with synthetic data first, or have you secured an authorised test customer?

## Product discovery (resolve with interviews)

6. Company sizes and staff roles: owner + manager + technicians sufficient?
7. Are jobs sometimes assigned to multiple technicians or subcontractors?
8. Can a customer own multiple sites and multiple AC units? (Current design assumes yes.)
9. What job status, service checklist and follow-up period are actually used?
10. What are the current systems and export formats for first prospective clients?
11. Which reminders (email, SMS, WhatsApp) are desired and what permission/consent process exists?
12. Do quotes/invoices need to stay in the client's existing accounting system?

## Commercial / operational (before pilots)

13. Subscription tiers, setup fee, trial length, billing currency, VAT/tax arrangements.
14. Hosting/data residency and contractual security/privacy requirements.
15. Support hours, backup recovery targets and client offboarding/export terms.
16. Human reviewer available for auth/RLS and production security checks?

## Decision rule

Record answers with date/source, update relevant documents, and mark approved choices in `DECISIONS.md`. If user guidance contradicts a proposed decision, the proposed decision must be revised rather than silently treated as fact.
