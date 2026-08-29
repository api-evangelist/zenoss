---
name: zenoss-maintenance-windows
description: Create, find and remove maintenance windows in Virtana Service Observability so planned work does not page anyone.
api: Virtana Service Observability API
generated: '2026-08-29'
method: generated
source: https://docs.zenoss.io/api/model-mgmt/maintenance-windows.html
operations:
  - POST /v1/modelcontext/maintwindows
  - PUT /v1/modelcontext/maintwindows
  - POST /v1/modelcontext/maintwindows:list
  - POST /v1/modelcontext/maintwindows:search
  - POST /v1/modelcontext/maintwindows:deleteBulk
  - POST /v1/modelcontext/entities:search
---

# Manage Zenoss maintenance windows

A maintenance window binds a schedule to a set of entities selected by an **entity query**, not by a
fixed list of IDs. Getting the query right is the whole job.

## Step 1 — prove the query selects what you think

`POST /v1/modelcontext/entities:search` with the same query you intend to use. Read the count and
spot-check the entities. A query that matches too broadly will silently suppress alerting on
unrelated infrastructure for the duration of the window.

`POST /v1/modelcontext/fields:listDefault` lists the default entity fields and their sources if you
need to know what is queryable.

## Step 2 — create the window

`POST /v1/modelcontext/maintwindows`. The response returns the window **IDs** — keep them. They are
the only handle for deletion later.

## Step 3 — verify

`POST /v1/modelcontext/maintwindows:list` or `:search`. Records come back with housekeeping fields
including `createdBy`, `updatedBy` and `deleted`, plus `pageInput`/`pageInfo` pagination.

Windows carry lifecycle states. Since April 2026 a window may report **Partially Completed** — it
finished the In Progress phase but could not be fully verified, usually because a change did not
reach a Collection Zone or a runtime error may succeed on rerun. Do not manually change Collection
Zone production states while a window is in that state; an automated rerun may overwrite you.

## Step 4 — edit or remove

- `PUT /v1/modelcontext/maintwindows` updates an existing window. The spec name cannot be changed —
  attempting it returns `400 (invalid request - for example, spec name update not allowed)`.
- `POST /v1/modelcontext/maintwindows:deleteBulk` takes `{"ids": [...]}` using the IDs from creation.

Deletion is reversible only in the sense that you can recreate the window from the same definition —
Zenoss publishes **no restore operation and no retention window** for deleted maintenance windows.
Keep your own copy of the definition before deleting.

## Legacy note

Collection Zone maintenance windows are a separate, deprecated feature. Retirement was announced for
2026-06-01 and then postponed in May 2026 with no new date. New work belongs on
`/v1/modelcontext/maintwindows`. See https://docs.zenoss.io/admin/updates/deprecation.html.
