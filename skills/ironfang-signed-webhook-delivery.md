---
name: renderwolf-signed-webhook-delivery
description: >-
  Register a Renderwolf delivery destination (signed webhook or your own S3-compatible bucket),
  attach it to jobs, verify the HMAC signature correctly, and handle the retry ladder — so
  finished renders arrive instead of being polled for.
api: Renderwolf API
base_url: https://api.ironfang.uk/renderwolf
operations:
  - createDestination
  - listDestinations
  - getDestination
  - updateDestination
  - deleteDestination
  - testDestination
  - listDeliveries
  - getDelivery
  - redeliverDelivery
  - submitJob
  - submitBatch
generated: '2026-09-02'
method: generated
source: openapi/ironfang-openapi.yaml + https://ironfang.uk/renderwolf/docs
---

# Delivery destinations and signed webhooks

## Preconditions
An API key carrying the `renderwolf:destinations` scope.

## Steps

1. **Register the destination.** `createDestination` — `POST /v1/destinations`.
   - Webhook: `{ "type": "webhook", "name": "Production", "url": "https://hooks.example.com/renderwolf" }`
   - Storage: `{ "type": "s3", "bucket", "region", "access_key", "secret_key", "endpoint"?, "prefix"?, "path_style"? }`
     — anything S3-compatible works (AWS, Cloudflare R2, MinIO, Ceph). Scope the credentials to
     the prefix you give; they only ever need write access there.
   - `201` returns `id` and, for a webhook, `signing_secret`. **The secret is shown exactly
     once.** Ironfang keeps only an encrypted copy and has no endpoint that can return it. Store
     it before you do anything else; if you lose it, your only option is a new destination — and
     every receiver must then be updated with the new secret.

2. **Prove the path works before a real job depends on it.** `testDestination` —
   `POST /v1/destinations/{id}/test`. It sends a real test delivery now and reports what
   happened. A receiver that does not answer is reported as a fact, not as an error.

3. **Attach it to work.** On `submitJob` or `submitBatch`, add
   `"delivery": { "webhook_destination": "<id>", "storage_destination": "<id>", "storage_key": "captures/{date}/{external_id}.png" }`.
   Credentials never travel in a job body — only the destination id.
   - `storage_key` accepts fixed text plus `{job_id}`, `{external_id}` and `{date}` (`YYYY/MM/DD`)
     and nothing else; nothing is evaluated. Default is `renderwolf/{date}/{job_id}`. A key that
     would climb out of the prefix is refused at submission, not silently rewritten.

4. **Verify every webhook.** Events are `render.job.succeeded`, `render.job.failed`,
   `render.job.cancelled` and `render.delivery.failed`.

   ```
   expected = "v1=" + hmac_sha256(secret, timestamp + "." + raw_body).hexdigest()
   compare(expected, headers["Renderwolf-Signature"])   # constant time
   ```

   - **Compute over the raw bytes you received**, never over a body you parsed and
     re-serialised. This is the single most common way this check is implemented wrongly.
   - `Renderwolf-Timestamp` is Unix seconds — reject anything more than a few minutes old to
     stop a replay.
   - `Renderwolf-Event-Id` is stable across retries of the same delivery. Key your handler's
     dedupe on it.
   - The success body carries the result's content type, size, SHA-256 and a signed `url` good
     for **15 minutes from the moment we sent it**, not from when the job finished. Fetch
     promptly or re-read the job for a fresh link.

5. **Handle the retry ladder.** Ironfang retries `408`, `429` and `5xx` from one minute out to
   a day with jitter, honouring a bounded `Retry-After` you send. Any other `4xx` stops
   immediately — that is your endpoint saying a retry will not help. After **10 consecutive
   failures the destination is disabled** until you re-enable it in the portal. Return `2xx`
   fast and do the work asynchronously.

6. **Audit what happened.** `listDeliveries` / `getDelivery` (which returns the body that was
   posted) / `redeliverDelivery` to send one again.

## Rules that matter here

- **Delivery never changes a render.** A job that rendered is `succeeded` whatever your endpoint
  did. An unreachable webhook does not spend a render attempt, hold a render slot, or turn a
  successful job into a failed one.
- **Storage failures reach you over the webhook.** If a storage delivery gives up, the webhook
  destination receives `render.delivery.failed` naming the destination and the error. That is
  how you find out a bucket stopped accepting uploads without watching for absent files.
- **Uploads are idempotent.** An object already present with the same checksum is left alone, so
  a retried delivery is a no-op rather than a second write.
- **Deleting is not undoable.** `deleteDestination` forgets the destination and its secret.
  Prefer `updateDestination` to disable it if you may want it back.
- **Agents cannot register storage destinations.** Through the MCP server only webhook
  destinations can be created; anything carrying credentials is portal-only, by design.
