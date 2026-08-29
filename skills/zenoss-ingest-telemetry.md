---
name: zenoss-ingest-telemetry
description: Send metrics, events and entity models into Virtana Service Observability (Zenoss Cloud) through the data receiver service, or through an OpenTelemetry collector.
api: Virtana Service Observability API
generated: '2026-08-29'
method: generated
source: https://docs.zenoss.io/api/receiver/data-receiver.html
operations:
  - POST /v1/data-receiver/metrics
  - POST /v1/data-receiver/events
  - POST /v1/data-receiver/models
  - grpc DataReceiverService.PutMetrics
  - grpc DataReceiverService.PutEvents
  - grpc DataReceiverService.PutModels
---

# Ingest telemetry into Zenoss

## Before you start

- Get a **Streaming Data Ingest** API key from `ADMIN > API Clients`. The other two key types
  (User Management API, User API) will not authorize the data receiver.
- Find your endpoint. There is no universal base URL — the API address field on the
  `ADMIN > API Clients` page shows yours. Production endpoints are `api.virtana.ai` (Iowa),
  `api2.virtana.ai` (Las Vegas), `api3.virtana.ai` (Sydney), `api4.virtana.ai` (Frankfurt).
- Every request needs `zenoss-api-key: <key>` and `content-type: application/json`.

## Step 1 — model the entity first

Telemetry is joined to entities by its **dimension map**, not by an ID. Send the model before or
alongside the metrics so the dimensions resolve to something.

`POST /v1/data-receiver/models` — body carries `models[]`, each with `timestamp`, `dimensions`
(a string→string map) and `metadataFields`. This is an upsert: the operation is documented as
"create or update entities".

## Step 2 — send metrics

`POST /v1/data-receiver/metrics`. Three wire shapes exist and they are not interchangeable:

- `metrics[]` — full form: `metric`, `timestamp`, `value`, `dimensions`, `metadataFields`.
- `taggedMetrics[]` — `metric`, `timestamp`, `value`, `tags`.
- `compactMetrics[]` — `id`, `timestamp`, `value`, referencing a metric already registered through
  the data registry service.

Use the same dimension keys you used for the model. Inconsistent dimensions create a second entity
rather than an error.

## Step 3 — send events

`POST /v1/data-receiver/events` — `events[]` with `name`, `timestamp`, `dimensions`, `type`,
`summary`, `body`, `severity` and `status`. Severity and status travel as integers.

## Step 4 — check the response, do not trust the status code

The data receiver documents `200 (full or partial success; see response message)`. The response is a
`StatusResult` / `EventStatusResult` / `ModelStatusResult` carrying a `message` plus
`failedMetrics[]`, `failedTaggedMetrics[]`, `failedCompactMetrics[]`, `failedEvents[]` or
`failedModels[]`. A 200 with a non-empty failure array means part of your batch was dropped.
Always read the arrays.

## Retry rules

- There is **no idempotency key** on this API. Metric and event writes are appends, so a blind retry
  after a timeout can double-count. Prefer resending only the entries named in the failure arrays.
- Model writes are upserts keyed on dimensions, so retrying those is safe.
- No rate limits, no `429`, and no `Retry-After` are documented. Back off on `500` on your own
  schedule.

## Alternative: OpenTelemetry

If your workload already exports OTLP, skip this API. Point an OpenTelemetry collector at
`https://api.zenoss.io:443` with exporter type `OTLP` and header
`zenoss-api-key=YOUR-ZENOSS-API-KEY`. Sum, gauge and histogram metrics are supported.
See https://docs.zenoss.io/streaming/open-telemetry.html.

## Alternative: gRPC

The same operations exist as gRPC RPCs with published proto3 contracts —
`PutMetrics`/`PutEvents`/`PutModels` (unary) and `PutMetric`/`PutEvent`/`PutModel`
(client-streaming). See `grpc/zenoss-data-receiver.proto` or
https://github.com/zenoss/zenoss-protobufs.
