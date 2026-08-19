---
name: Build and share a Bynder collection
description: >-
  Create a collection, add and remove assets, read its contents, and share it with
  other users — the standard curation flow for handing a set of approved assets to
  a team or an external partner.
api: openapi/bynder-collections-v4-openapi.json
operations:
  - "GET /api/v4/collections"
  - "POST /api/v4/collections"
  - "GET /api/v4/collections/{id}"
  - "POST /api/v4/collections/{id}"
  - "DELETE /api/v4/collections/{id}"
  - "GET /api/v4/collections/{id}/media"
  - "POST /api/v4/collections/{id}/media"
  - "DELETE /api/v4/collections/{id}/media"
  - "POST /api/v4/collections/{id}/share"
generated: '2026-08-13'
method: generated
source: openapi/bynder-collections-v4-openapi.json
---

# Build and share a Bynder collection

A collection is Bynder's unit of hand-off: an ordered, shareable set of assets.

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

1. **Check for an existing collection first.** `GET /api/v4/collections`
   (scope `collection:read`). Because there is no idempotency key, creating
   blindly is how duplicates appear. Search by name before you create.

2. **Create.** `POST /api/v4/collections` with the name and description.
   Requires scope `collection:write` and the `COLLECTIONS` security role.

3. **Add assets.** `POST /api/v4/collections/{id}/media` with the asset ids.
   Use ids exactly as returned by `GET /api/v4/media/` — do not reformat them.

4. **Read back.** `GET /api/v4/collections/{id}/media` to confirm membership,
   and `GET /api/v4/collections/{id}` for the collection itself.

5. **Remove assets.** `DELETE /api/v4/collections/{id}/media`.

6. **Share.** `POST /api/v4/collections/{id}/share` with the recipients and the
   permission level. Requires the `SHARECOLLECTION` role; public sharing
   additionally needs `PUBLICCOLLECTIONS` / `PUBLISHCOLLECTIONS` depending on how
   the portal is configured.

7. **Delete.** `DELETE /api/v4/collections/{id}` removes the collection.
   It does not delete the assets in it.

## Failure handling

- **403 on share** — the profile lacks `SHARECOLLECTION` or one of the public
  collection roles. Report which.
- **404 on add** — an asset id in the batch does not exist in this portal.
  Bynder does not always tell you which one; add in smaller batches to isolate it.
- **Duplicate collections after a timeout** — re-run step 1 and merge, then delete
  the duplicate. There is no idempotency key to prevent this.
