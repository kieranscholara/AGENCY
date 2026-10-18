# SaaS Billing and Plans

**Status:** Future milestone; no live prices, Stripe account or subscription integration are assumed.

## Business model

Your agency operates one SaaS. AC companies subscribe to use a private company workspace. Their own service customers do not subscribe to the SaaS.

## Pricing hypotheses (not validated)

Examples to test: Starter €49/month, Professional €99/month, Business €199/month. Decide limits and VAT/tax treatment with appropriate advice. Avoid custom pricing code scattered through React components.

## Billing architecture

- Stripe Billing/hosted Checkout for subscription signup, where available and appropriate.
- Server creates checkout session tied to verified organisation and authorised owner.
- Verified Stripe webhooks update local subscription state. Never unlock access on browser redirect alone.
- Check event signatures, record event IDs, handle retries/out-of-order events, reconcile state periodically.
- Keep provider customer/subscription IDs in server-controlled tables.
- Implement explicit trial, active, past_due, cancelled/ended states with documented grace periods and access behaviour.

## Access and usage

Enforce plan restrictions on server services, not CSS/UI only. Usage measures can include staff seats, storage, notification volume and active units/jobs where validated. Prefer graceful read-only access and export options over sudden inaccessible client records after cancellation.

## Admin operations

Operator can see billing status and manage plan support workflows but must not need full access to unrelated private service records. Record admin changes in an audit trail.

## Before launch

Confirm final plans and VAT implications, consumer/business terms, refunds/cancellations, trial handling, invoice requirements, payment failure policy, and access after subscription termination.
