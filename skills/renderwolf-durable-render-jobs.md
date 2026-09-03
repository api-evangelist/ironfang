---
name: renderwolf-durable-render-jobs
description: >-
  Run Renderwolf renders as durable jobs — submit with an idempotency key, poll or receive a
  signed webhook, collect the result inside its 24-hour window, and cancel safely — the correct
  pattern for agents, batches and anything slow.
api: Renderwolf API
base_url: https://api.ironfang.uk/renderwolf
operations:
  - submitJob
  - listJobs
  - getJob
  - cancelJob
  - getJobResult
  - getSignedResult
  - submitBatch
  - getBatch
generated: '2026-09-02'
method: generated
source: openapi/renderwolf-openapi.yaml + https://ironfang.uk/renderwolf/docs
---

# Durable render jobs

## When to use this
Clips, slow pages, batches, and any agent-driven render. The synchronous endpoints
(`createScreenshot`, `createPdf`, …) hold a connection open and return bytes; a job does not.

## Steps

1. **Submit.** `submitJob` — `POST /v1/jobs` with header `Idempotency-Key: <your key>` and body
   `{ "kind", "request", "external_id"?, "delivery"? }`.
   - `kind` is one of `screenshot`, `pdf`, `qr`, `image`, `clip`, `site_preview`.
   - `request` is exactly that endpoint's body. An `image` job names its `template` inside
     `request`.
   - **Always send `Idempotency-Key`.** Same key + same request returns the existing job. Same
     key + a different request is `409 idempotency_conflict`. This header is documented but is
     NOT in the OpenAPI, so a generated client will not send it for you — add it yourself.
   - The submission is validated exactly as the synchronous endpoint would validate it *before*
     anything is charged.
   - Returns `202` with a job envelope: `job_id`, `status`, `kind`, `cached`,
     `credits: { reserved, charged }`, `created_at`.

2. **Poll.** `getJob` — `GET /v1/jobs/{id}`. `status` is `queued`, `running`,
   `cancellation_requested`, `succeeded`, `failed` or `cancelled`. A succeeded job carries
   `result` with content type, byte size, SHA-256 and expiry, plus a signed `url` valid for
   **15 minutes** that needs no API key.

3. **Collect.** `getJobResult` — `GET /v1/jobs/{id}/result` redirects (`302`) to a fresh signed
   link; `getSignedResult` — `GET /v1/results/{exp}/{sig}` is that link. **The hosted result is
   kept 24 hours after success and then removed.** This is a collection window, not asset
   hosting — store what you need on your side. `410` means it is gone.

4. **Cancel when you must.** `cancelJob` — `DELETE /v1/jobs/{id}`. A queued job stops at once
   and is refunded in full. A running job stops at its next safe point and is charged only if
   it produced a usable output. `409` if it already reached a terminal state.

## Batches

`submitBatch` — `POST /v1/batches` with the same `Idempotency-Key` discipline: a shared
`default` request plus up to 100 `items` that override parts of it. The merge is one level
deep — an item's field wins, everything else comes from `default`. An item may override `kind`
and carry its own `delivery`.

A batch is accepted or refused **whole**: every item is validated before any is stored and the
credits for all of them are reserved in one transaction, so a batch that would exceed your
monthly credits comes back `429 quota_exhausted` having charged nothing and left no jobs
behind. A validation error names the item it came from.

Poll `getBatch` — `GET /v1/batches/{id}` for `counts` by state, `done`, and the full job
resource for every item. **There is no batch-level cancel** — cancel items individually. There
is no ZIP of results either; use a storage destination when the batch is large.

## Credits and reversibility

- The job's **maximum** cost is reserved on acceptance and settled on completion — a site
  preview reserves the 60-second ceiling and releases the difference once the page is measured.
- Failed work is refunded. A queued job cancels for free.
- Transient failures are retried up to three times with backoff; a page that refuses to render
  fails at once with the reason.

## Rate limits and errors
`429` with `rate_limited` (120/min per account), `target_rate_limited` (60/min per target host,
across all customers) or `quota_exhausted` (plan cap — pauses, never charges overage). No
`RateLimit-*` or `Retry-After` headers are published, so back off on the status code.
Errors are `{"error": {"code", "message"}}`; branch on `code` only.
