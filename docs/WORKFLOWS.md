# User Workflows

These are intended flows, not evidence of implemented features.

## 1. Company onboarding

1. Business owner requests subscription/trial.
2. Backend establishes unique organisation in a transaction with an authorised owner membership.
3. Owner verifies identity and configures company timezone/contact preferences.
4. Owner invites staff; each invitation has scoped expiry and a single-use or otherwise safe acceptance process.
5. Owner optionally imports existing customer/equipment records after reviewing a dry run.

## 2. Office manager books a service

1. Search or create customer; select service address and AC unit.
2. Choose visit type, time, assigned technician and special instructions.
3. Backend verifies all referenced resources are in the active organisation and checks relevant scheduling constraints.
4. Job is saved with an initial history entry.
5. Optionally enqueue approved customer/technician notification after the transaction is committed.

## 3. Technician completes service

1. Log in on mobile and open authorised assigned job.
2. Check service details and add condition notes/checklist.
3. Upload photos using short-lived, job-bound authorisation to private storage.
4. Submit report; backend verifies current status/ownership and uses safe transaction boundaries.
5. Record completion time and next service date if the company has configured a valid interval.
6. Report becomes available to authorised staff; reminder generation is processed asynchronously.

## 4. Reminder lifecycle

Daily job finds eligible service dates → confirm reminders aren't already scheduled/sent → generate dispatch record → deliver through authorised provider → store provider result → safely retry errors. Contacts with no valid communication preference/basis are not messaged.

## 5. Import/migration

Client-authorised CSV/Excel export → secure temporary upload → parse and map columns → validate / deduplicate → present preview and errors → explicit approval → idempotent import → reconciliation report. Record import operator and timestamp. Offer export before destructive changes.

## 6. Cancellations, exceptions and disputes

Specify who may reschedule, cancel, correct a completed report, and export records. Corrections to completed service records should preserve prior information for audit rather than silently rewriting history.
