---
name: Upload a file and save it as a Bynder asset
description: >-
  Run Bynder's chunked upload sequence end to end — request an upload endpoint,
  initialise the upload, push chunks, poll for processing, and finalise the file
  as a new asset or as a new version of an existing asset.
api: openapi/bynder-asset-upload-openapi.json
operations:
  - "GET /api/upload/endpoint"
  - "POST /api/upload/init"
  - "POST /api/v4/upload/{id}"
  - "GET /api/v4/upload/poll"
  - "POST /api/v4/media/save/{importId}"
  - "POST /api/v4/media/{id}/save/{importId}"
generated: '2026-08-13'
method: generated
source: >-
  openapi/bynder-asset-upload-openapi.json and
  openapi/bynder-modern-stack-upload-openapi.json
---

# Upload a file and save it as a Bynder asset

Bynder upload is a multi-step, stateful sequence, not a single POST. Every step
must complete in order and the whole sequence is **not idempotent** — this is the
flow where retrying blindly creates duplicate assets.

## Before you call anything

- **Base URL is per customer.** Every Bynder call goes to the customer's own portal
  host, `https://{your-bynder-domain}` (for example `https://acme.bynder.com`).
  There is no shared Bynder API hostname. Ask for the portal domain before you start.
- **Two authorization layers.** An OAuth scope is necessary but not sufficient.
  Bynder also enforces named security roles from the user's security profile.
  A 403 on a call you hold the scope for means the profile is missing the role —
  do not retry, escalate to a portal admin.
- **Two id formats.** `/api/v4/*` uses ColdFusion UUIDs (8-4-4-16);
  `/api/*` without `/v4` uses RFC 4122 UUIDs (8-4-4-4-12). Passing one where the
  other is expected returns 404, not 400. Never reformat an id — pass back exactly
  what the API gave you.
- **Rate limit: 4500 requests / 5 minutes / source IP, no headers.** Bynder returns
  no `X-RateLimit-*`, no `RateLimit-*` and no `Retry-After`. You cannot read your
  remaining budget. Self-throttle to about 10 requests/second. On a 429, stop for a
  full five minutes — further requests extend the block.
- **No idempotency.** Bynder publishes no `Idempotency-Key`. A POST that times out
  may or may not have succeeded. Before retrying any create, re-read the collection
  or list endpoint and check whether the object already exists.
- **No 429 in the specs.** The published OpenAPI definitions declare 400/401/403/404/409/500
  but never 429. Handle 429 defensively even though the contract does not mention it.

## Steps

1. **Get the upload endpoint.** `GET /api/upload/endpoint` returns the closest S3
   upload endpoint for this portal. Do not hardcode it; it varies by region.

2. **Initialise.** `POST /api/upload/init` with the filename. The response carries
   the upload identifiers you use for the rest of the sequence.
   Requires scope `asset:write` and the `MEDIAUPLOAD` security role
   (`MEDIAUPLOADFORAPPROVAL` where the portal routes uploads through approval).

3. **Push chunks.** Upload each chunk to the S3 endpoint from step 1, then register
   it with `POST /api/v4/upload/{id}` giving the chunk number. Chunks must be
   registered in order.

4. **Poll for processing.** `GET /api/v4/upload/poll` with the import identifiers.
   Bynder processes the file asynchronously; do not proceed until it reports done.
   Poll on an interval, not in a tight loop — remember the 4500 requests / 5
   minutes / IP budget is shared with everything else on your egress address.

5. **Finalise — pick one.**
   - New asset: `POST /api/v4/media/save/{importId}` with brandId, name and any
     metaproperty values.
   - New version of an existing asset: `POST /api/v4/media/{id}/save/{importId}`.

## Modern Stack alternative

Newer portals expose a second upload surface on `/v7`:
`POST /v7/file_cmds/upload/prepare`,
`POST /v7/file_cmds/upload/{file_id}/chunk/{chunk_number}`,
`POST /v7/file_cmds/upload/{file_id}/finalise_api`
(`openapi/bynder-modern-stack-upload-openapi.json`). Use whichever the portal's
documentation says is current for that customer — do not mix the two sequences.

## Retry rules — read this before you retry anything

There is no idempotency key. If step 5 times out you do not know whether the asset
was created. **Before retrying a finalise, search for the asset**
(`GET /api/v4/media/` with the filename as `keyword`) and only retry if it is
absent. Steps 1–4 are safe to retry; step 5 is not.

## Failure handling

- **500 "Upload failed or not ready"** — the poll in step 4 had not completed.
  Go back to step 4.
- **403** — the profile lacks `MEDIAUPLOAD`.
