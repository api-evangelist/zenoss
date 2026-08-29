---
name: zenoss-triage-events
description: Search, count and analyse events in Virtana Service Observability (Zenoss Cloud), then acknowledge, annotate or close them.
api: Virtana Service Observability API
generated: '2026-08-29'
method: generated
source: https://docs.zenoss.io/api/event-mgmt/event-query.html
operations:
  - POST /v1/events:search
  - GET /v1/events/{id}
  - POST /v1/events:count
  - POST /v1/events:frequency
  - POST /v1/event-management/annotate
  - POST /v1/event-management/annotate-common
  - POST /v1/event-management/delete-annotations
  - POST /v1/event-management/status
  - POST /v1/event-management/status-common
---

# Triage Zenoss events

Authenticate every call with `zenoss-api-key: <key>` against your assigned endpoint.

## Step 1 — find the events

`POST /v1/events:search`. The request is a structured query, not a query string:

- a **clause tree** — nested `And` / `Or` / `Equals` nodes over event fields such as `severity`,
  `status` and `source`;
- a time range;
- `activeCriteria` — `BY_TIMERANGE` (default; occurrences last updated inside the range);
- `fields[]` — name only the fields you want back;
- `pageInput` — `pageSize`, `cursor`, `direction` (`DIRECTION_FORWARD` default).

The response carries `pageInfo` with `count`, `totalCount`, `hasNext`, `startCursor` and
`endCursor`. Page forward by feeding `pageInfo.endCursor` back as `pageInput.cursor`.

## Step 2 — size the problem before you act

- `POST /v1/events:count` returns a count for the same clause query — cheaper than paging when you
  only need the number.
- `POST /v1/events:frequency` buckets occurrences over the range, which is what tells you whether
  you are looking at one flapping entity or a real fan-out.

Do this before any bulk status change. There is no undo across a bulk operation.

## Step 3 — read one event

`GET /v1/events/{id}` with the opaque id from the search results
(for example `AAAABg6X6wV4Sv-3-zQ7kcxJaqg=`).

## Step 4 — annotate and set status

- `POST /v1/event-management/annotate` attaches a note. `annotate-common` applies one note to a set.
- `POST /v1/event-management/status` changes status. `status-common` applies one status to a set.

Both are reversible: `POST /v1/event-management/delete-annotations` removes annotations, and status
is a mutable field you can set back to its previous value. Neither has a published time window, so
capture the prior status yourself before changing it if you may need to restore it.

## Error handling

Failures return `{"code": <int>, "message": "<text>"}` — the gRPC status shape, not
`application/problem+json`. Expect `400` on an empty search input, `401` on a missing or invalid key,
`404` for an unknown id, and `500` for server faults. There is no stable machine-readable error slug,
so branch on the HTTP status, not on the message text.
