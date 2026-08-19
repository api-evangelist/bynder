---
name: Find an asset and get its download URL
description: >-
  Search a Bynder portal for an asset by keyword, type, brand or metaproperty,
  read its metadata, and obtain a time-limited download location for the original
  file, a specific version, or a specific asset item.
api: openapi/bynder-asset-v4-openapi.json
operations:
  - "GET /api/v4/media/"
  - "GET /api/v4/media/{id}"
  - "GET /api/v4/media/{id}/download"
  - "GET /api/v4/media/{id}/{version}/download"
  - "GET /api/v4/media/{id}/download/{itemId}"
  - "POST /api/1/assets/similarity-search/"
generated: '2026-08-13'
method: generated
source: >-
  openapi/bynder-asset-v4-openapi.json, openapi/bynder-asset-download-openapi.json,
  openapi/bynder-similar-assets-openapi.json
---

# Find an asset and get its download URL

The most common Bynder integration: locate an approved asset and hand a caller a
URL they can fetch.

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

1. **Search.** `GET /api/v4/media/` with `keyword`, `type`
   (`image` / `document` / `audio` / `video`), `brandId`, metaproperty filters,
   `orderBy`, `page` and `limit`.
   Requires scope `asset:read`.
   Read `X-Pagination-TotalRecords`, `X-Pagination-TotalPages`, `X-Pagination-Page`
   and `X-Pagination-Limit` from the **response headers** — the totals are not in
   the body. Page with `page` + `limit`.

2. **Read the asset.** `GET /api/v4/media/{id}` returns the asset with its
   metaproperty values, tags, derivatives and `additionalId` items.
   Requires scope `asset:read`.

3. **Optional — find lookalikes.** `POST /api/1/assets/similarity-search/`
   returns assets similar to a reference asset. Note this is on the `/api/1`
   surface, so it takes an **RFC 4122 UUID**, not the `/api/v4` ColdFusion id.

4. **Get the download location.**
   - Original: `GET /api/v4/media/{id}/download`
   - A specific version: `GET /api/v4/media/{id}/{version}/download`
   - A specific item within the asset: `GET /api/v4/media/{id}/download/{itemId}`

   All three return a **time-limited** URL. Fetch it promptly; do not cache or
   persist it as a permanent asset address.

## The role wall on downloads

Download is the operation where Bynder's second authorization layer bites hardest.
Beyond `asset:read`, the user's security profile must carry:

| Condition | Required role |
|---|---|
| Always | `MEDIAHIGHRES` |
| Asset is archived | `ARCHIVEDOWNLOAD` |
| Asset is watermarked | `DOWNLOADWATERMARK` |
| Asset is marked limited-usage / key visual | `KEYVISUALSDOWNLOAD` |

A 403 here is a profile problem, not a token problem. Report which of these four
roles is likely missing rather than retrying.

## Failure handling

- **404** — most often the id came from the wrong surface. `/api/v4` ids are
  8-4-4-16; `/api/1` ids are 8-4-4-4-12.
- **403** — see the role table above.
- **429** — stop for five minutes. There is no `Retry-After` to read.
