---
name: zenoss-notification-actions
description: Wire Zenoss Actions — triggers, rules and destinations — so events reach a webhook, Slack, PagerDuty, ServiceNow or Teams.
api: Virtana Service Observability API
generated: '2026-08-29'
method: generated
source: https://docs.zenoss.io/api/actions/actions.html
operations:
  - POST /v1/notification/triggers
  - GET /v1/notification/triggers/{name}
  - PUT /v1/notification/triggers/{name}
  - DELETE /v1/notification/triggers/{name}
  - POST /v1/notification/destinations
  - POST /v1/notification/destinations:test
  - PUT /v1/notification/destinations/{name}
  - DELETE /v1/notification/destinations/{name}
  - POST /v1/notification/rules
  - GET /v1/notification/rules
  - PUT /v1/notification/rules/{name}
  - DELETE /v1/notification/rules/{name}
  - POST /v1/credentials
---

# Set up Zenoss Actions notifications

Actions is three objects: a **trigger** (what condition fires), a **destination** (where the message
goes) and a **rule** (which triggers feed which destinations, with what message and repeat interval).
All three are addressed **by name** in the path, so pick names you can live with — renaming is not
supported.

## Step 1 — store any credential the destination needs

`POST /v1/credentials` for ServiceNow OAuth, Slack, Microsoft 365, Zoom, PagerDuty or an API key.
`GET /v1/credentials` lists them (paginated with `nextPageToken` — note this service uses a page
token, not the `pageInfo` cursor the search APIs use).

## Step 2 — create the destination

`POST /v1/notification/destinations`. A generic `webhook` destination takes a URL, custom headers,
and optionally a custom JSON payload. There is **no signature or shared-secret scheme**, so if the
receiver needs to authenticate Zenoss, put a token in the custom headers yourself.

## Step 3 — test it before wiring anything to it

`POST /v1/notification/destinations:test` sends a test message. This is the only dry-run affordance
on the API — use it, because a misconfigured destination fails silently at 3am otherwise.

## Step 4 — create the trigger

`POST /v1/notification/triggers`. Trigger types are event, metric threshold, anomaly, maintenance
state and stale data. Event triggers take the same clause grammar as event search — nested
`And`/`Or`/`Equals` over fields like `severity`, `status` and `source`.

## Step 5 — create the rule

`POST /v1/notification/rules` with `trigger_names[]`, `destination_names[]`, a `message`, `enabled`
and `repeat_interval` (seconds). `repeat_interval` is your only throttle: without it a noisy trigger
will fan out on every occurrence.

## What the receiver gets

The delivered JSON carries `id`, `tenant`, `timestamp`, the full `rule`, the full `trigger`
definition including its clause tree, and the matched `event` with `summary`, integer `severity`,
integer `status` and a fields map containing internal keys (`_zen_clientid`,
`_zen_direct_entity_id`, `_zen_entityIds`). No retry or delivery-guarantee semantics are published.
See `asyncapi/zenoss-webhooks.yml`.

## Teardown

Each object has a `DELETE .../{name}`. Delete rules before the triggers and destinations they
reference. There is no restore and no retention window.
