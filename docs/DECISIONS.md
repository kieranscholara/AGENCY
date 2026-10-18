# Architecture and Product Decisions

Record **approved** decisions, not every AI suggestion. Significant changes should have their own ADR in `docs/decisions/`.

| ID | Decision | Status | Reason / review trigger |
| --- | --- | --- | --- |
| D-001 | Aim for one multi-tenant SaaS product for AC service companies | Proposed | Fits subscription model; validate customer demand |
| D-002 | Use modular monolith rather than microservices for MVP | Proposed | Minimises cost/operational complexity |
| D-003 | Use Next.js + TypeScript + Supabase as initial stack | Proposed | Consistent with prior planning; verify real codebase |
| D-004 | Enforce tenant isolation at API and database levels | Required invariant | Protects company records and customer privacy |
| D-005 | Prioritise CSV onboarding before broad third-party integrations | Proposed | Smallest practical migration workflow |
| D-006 | Introduce paid billing only when onboarding is validated | Proposed | Avoid building subscription features before product workflow |

## Decision lifecycle

`Proposed → Approved / Rejected → Superseded`. An approved decision includes date, owner, rationale, alternatives, consequences, affected files/migrations, and acceptance/test evidence.

## New decision template

Use `docs/decisions/ADR_TEMPLATE.md`. Link the ADR here after approval. Avoid changing `AGENTS.md` or security rules by implication in a chat message without documenting the change.
