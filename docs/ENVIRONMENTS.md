# Environments, Configuration and Secrets

## Environment policy

| Environment | Use | Data | Credentials |
| --- | --- | --- | --- |
| Local | Development | Synthetic | Local/test only |
| Staging | Integration/E2E and client demo | Synthetic/anonymised | Dedicated staging |
| Production | Real subscribers | Personal/business | Dedicated production |

Use separate Supabase projects/databases/storage/auth instances for staging and production. Stripe test and live modes must be isolated. Do not point preview deployments at the production database.

## Proposed initial variable categories

Verify exact keys from installed libraries/template. Examples only:

```dotenv
NEXT_PUBLIC_SUPABASE_URL=...          # Public endpoint
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY=... # Public publishable key
# Server-only secrets, when required, supplied through secret manager:
# STRIPE_SECRET_KEY / STRIPE_WEBHOOK_SECRET
# RESEND_API_KEY
# INNGEST_EVENT_KEY / INNGEST_SIGNING_KEY
```

Publishable values are not a substitute for RLS. Never commit secret values. `.env.local` is local and gitignored; an `.env.example` may contain names and placeholders only. Supabase privileged keys belong only in trusted server environments with minimal exposure.

## Operational practices

- Document base URL, permitted domains and webhook endpoints per environment.
- Configure auth redirects/email templates carefully for each environment.
- Track migrations applied in each environment; don't edit applied history.
- Limit who can view runtime secrets or download database backups.
- Remove access promptly when a contractor leaves.
- Keep client production data away from AI tools unless explicitly authorised and supported by appropriate protections.

## Before first production deploy

Confirm database/storage isolation, email sending domain, backup plan, error monitoring, acceptable data region, webhook verification, restricted admin access and rollback path.
