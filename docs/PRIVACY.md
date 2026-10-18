# Privacy and Data Handling (Planning Document)

This is an engineering checklist, **not legal advice**. Confirm GDPR/controller/processor obligations, contracts and retention with qualified counsel before processing real client personal data.

## Data categories

Business employees' identities, roles and activity; service customers' contact details and addresses; equipment/serial numbers; notes/photos from sites; appointment and communications history; payment metadata for business subscriptions.

## Key questions to resolve

- Is the AC firm controller for its customer data, with the SaaS operator acting as processor? Define this accurately in agreements.
- What lawful basis and communication preferences apply to service reminders versus marketing?
- Which data needs retention after contract termination or customer deletion requests?
- Which subprocessors/processors and hosting regions are used (Supabase, Vercel, Stripe, email provider etc.)?
- How will exports, deletion requests, access requests and incidents be handled?

## Engineering requirements

- Collect only fields needed for documented service workflows.
- Encrypt in transit, apply least privilege, tenant isolation and secure storage.
- Don't use customer names, addresses, photos or service logs in AI prompts or development fixtures without authorisation and proper protections.
- Avoid logging request bodies with personal information.
- Support export and reasonable retention/erasure lifecycle, including objects in Storage and backups where technically applicable.
- Have terms, privacy notice, a data processing agreement and subprocessor information before production onboarding.
- Do not send automated reminders unless the company has configured appropriate contact preferences and legal basis.

## Retention schedule (TBD)

Define by data class: accounts, job history, photos, audit logs, import source files, temporary uploads, backups and billing records. Record approved schedule and automated deletion behaviour here before launch.
