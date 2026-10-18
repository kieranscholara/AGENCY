# First Client Import and Data Migration Runbook

**Goal:** Transfer authorised customer and equipment records without losing or silently modifying source data. No live client import before signed permission/DPA and secure environments.

## Client preflight

- Confirm exact existing system, admin/export rights, customer/AC-unit count, site addresses, service history and sample formats.
- Identify authoritative system during pilot and cutover. Decide whether changes continue in old system or are frozen.
- Request *anonymised* 10–20 row sample first; document actual column mapping and uniqueness/duplicate rules.
- Confirm whether reminders can legally be sent; imported phone/email addresses are **not automatic marketing consent**.

## Staged import flow

1. Store client-approved source file in private temporary bucket with short retention and access logging.
2. Validate CSV encoding, field lengths, types, row limits and CSV formula injection; never execute imported formulas or scripts.
3. Map contact/customer/site/equipment fields; present transform preview and unrecognised values.
4. Detect potential duplicate customers and AC units; create operator review rather than silently merge ambiguous matches.
5. Client approves preview with record counts and notable exclusions.
6. Commit in transaction/chunks with idempotent import row keys; do not create cross-org relationships.
7. Produce reconciliation: source rows vs created/updated/skipped/invalid; sample check customer/equipment chain and service dates.
8. Client signs reconciliation; archive/delete original upload per retention; log import actor/date/schema version.

## Go/no-go data thresholds

No silently lost records; 100% counted in reconciliation; all validation exceptions reviewed or explicitly approved for exclusion. Sample spot checks include multiple AC units at one site, same customer across sites, date/time formats, repeated phone numbers, missing serials.

## Rollback and cutover

Maintain source export encrypted and immutable for agreed limited window. Tag all imported rows with batch ID. A rollback is **not** blind DELETE when imported records acquired new job history; propose audited compensation plan, test on staging and get client approval. Run final delta import if existing system remains active.
