# Customer Onboarding and Data Migration

## Goal

Make it possible for an AC company to start without re-entering all its customers and installed equipment. Never connect to existing client systems or import customer data without client authorisation.

## Onboarding checklist

1. Confirm subscription/pilot agreement, terms, data processing arrangement and primary business owner.
2. Create one tenant; invite and verify owner; configure business name, timezone and branding.
3. Establish staff role policy and invite authorised employees.
4. Ask what they currently use (Excel, WhatsApp, paper, accounting, CRM, field service application).
5. Decide migration route: manual, CSV/Excel, or official API connector.
6. Run a sample data import to staging/test environment using synthetic or approved data.
7. Run validation/deduplication and have the client sign off on preview counts and sample records.
8. Import to the right production tenant, reconcile source and destination counts, log failed rows.
9. Verify customer contacts, units, upcoming visits, staff permissions and report generation with client.
10. Activate approved notifications; deliver short staff training and support contact.

## Proposed CSV fields

Customers: customer external reference, name, phone/email, address. Equipment: external reference, customer reference, service site, manufacturer, model, serial, installation date, last service date and maintenance interval. Additional columns require explicit mapping decisions.

## Import rules

Never silently overwrite an existing contact. Prefer stable external references; otherwise use reviewable duplicate suggestions. Track import batch ID, uploader, tenant, record mapping, errors and reconciliation. Design a safe recovery/reversal plan before committing a large import.

## First-week check-in

Review number of jobs entered, technicians activated, import issues, missed reminders and feedback. Record only verified results, not guessed ROI.

## Offboarding

Define and contractually honour export format, retention, access termination, deletion workflow and handling of external integrations. No arbitrary platform access to client data after offboarding.
