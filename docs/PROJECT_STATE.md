# Project State — Verified Facts Only

**Last updated:** 2026-10-18 (initial document pack; repository not inspected)
**Current milestone:** M0 — Repository and documentation setup
**Overall status:** UNVERIFIED

## Confirmed in conversation

- The intended first product is a multi-tenant AC servicing SaaS.
- The intended development approach uses VS Code, GitHub, Codex and Claude Code.
- Next.js + Supabase was the proposed starting architecture.

## Not yet verified

- [ ] GitHub repository exists and is private
- [ ] Actual frontend framework and package versions
- [ ] `package.json` scripts and installed dependencies
- [ ] Local application starts successfully
- [ ] Supabase development project connected
- [ ] Auth/signup works
- [ ] Schema migrations exist and are applied
- [ ] RLS policies exist and pass tenant isolation tests
- [ ] Any production/staging deployment exists
- [ ] CI/lint/typecheck/test/build checks pass
- [ ] Any actual AC customer/pilot relationship exists

## Last verified commands

_None. Fill in actual command, date, exit status and environment after running._

## Last completed work

- Generated a proposed Markdown engineering documentation starter pack.
- No code changes, migrations, tests or deployments were performed as part of this pack.

## Current next actions

1. Inspect repository and document actual stack/state.
2. Confirm unresolved decisions in `OPEN_QUESTIONS.md`.
3. Verify development env/auth; add or adjust `.env.example` (without secrets).
4. Create M1 implementation plan and database RLS design.
5. Implement smallest verified vertical slice after approval.

## Open risks

- Codebase/framework might differ from assumed Next.js starter.
- Pricing and target company workflow have not been validated.
- Multi-tenant security needs independent verification before pilots.

## Update template

```text
Date:
Milestone:
Verified working:
Changed files:
Actual checks run + results:
Known failures:
Risks / outstanding decisions:
Next task:
```


## v2 document extension (not code evidence)

The detailed pilot architecture supplement has been drafted. **No new application code, tests, staging credentials, migrations, or actual client integrations have been executed or verified by creating this pack.** Run the read-only audit in `docs/GET_STARTED_WITH_CODEX.md` before changing any feature state to "working".
