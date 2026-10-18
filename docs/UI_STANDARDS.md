# UI/UX and Accessibility Standards

## Principles

Make the product fast and unambiguous for office staff and technicians. An organised business workflow is more valuable than decorative dashboards. Desktop first for office scheduling; mobile first for technician job reports.

## Proposed design stack

React/Next.js, Tailwind CSS and accessible shadcn/ui primitives (verify actual repo). Use shared components for inputs, tables, cards, dialogs, statuses, date/time entry, and destructive action confirmation.

## Mandatory view states

Every async page must specify loading, empty, success, recoverable error, permission denied and stale session states. Never render data from a previous tenant after switching organisations.

## Forms

Clear labels, required fields, server validation messages, keyboard navigation, useful defaults, save/cancel behaviour, duplicate-submit handling and protection against accidental data loss. Confirm timezone for appointments. Don't obscure failed requests behind generic toasts.

## Responsive layouts

- Office: customer list, calendar, jobs, equipment histories, quotes, settings.
- Technician: today's assigned jobs, equipment details, checklist, notes/photos, submit report.
- Prefer large tap targets, low-clutter views and accessible colour contrast.

## Branding

Neutral professional palette and business-friendly typography. Avoid hard-coded client brands in shared app UI; store per-organisation logo/name configuration with sanitised asset access. Custom theming is a later priority unless needed for pilots.

## Performance and trust

Use pagination and server filtering for large customer lists, avoid fetching entire tenant datasets, preserve input state after errors, clearly distinguish unsaved changes, and show when reminders or exports are pending rather than pretending the operation finished.
