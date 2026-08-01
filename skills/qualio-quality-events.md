---
name: Qualio quality events
description: Log and track quality events (CAPAs, deviations, non-conformances) and their templates in the Qualio QMS.
api: openapi/qualio-openapi.json
operations: [listEventTemplates, createEvent, queryEvents, getEvent]
---

# Qualio quality events

Create and monitor quality events in a Qualio tenant. API-key auth (`X-Api-Key`),
base URL `https://api.qualio.com`.

## Steps

1. **Pick a template** — `listEventTemplates` (`GET /v1/events/templates`) to choose the
   event type (e.g. CAPA, deviation, complaint).
2. **Raise the event** — `createEvent` (`POST /v1/events/events`) with the template and
   event details.
3. **Track** — `queryEvents` (`GET /v1/events/events`) to list/filter events and
   `getEvent` (`GET /v1/events/events/{code}`) to read a single event by its code.

## Rules
- Reference events by their human-readable `code`.
- Paginate with `offset`/`limit`; filter query params vary per endpoint.
- Handle `403`/`404`/`429` as in `errors/qualio-problem-types.yml`; no idempotency keys.
