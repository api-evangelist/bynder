---
name: Subscribe to Bynder asset and workflow events
description: >-
  Create and manage a Bynder webhook subscription so an agent is notified when
  assets are created, updated, archived or deleted, when a workflow job is
  created, or when an antivirus scan fails.
api: openapi/bynder-webhooks-openapi.json
operations:
  - RetrieveaWebhookConfiguration
  - CreateaWebhookConfiguration
  - UpdateaWebhookConfiguration
  - PatchaWebhookConfiguration
  - DeleteaWebhookConfiguration
generated: '2026-08-13'
method: generated
source: >-
  openapi/bynder-webhooks-openapi.json and
  https://api.bynder.com/reference/getwebhookconfigurations
---

# Subscribe to Bynder asset and workflow events

Polling `GET /api/v4/media/` for changes burns the per-IP rate budget fast.
Webhooks are the right mechanism — with the caveats below.

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

## The events Bynder publishes

| Event | Fires when |
|---|---|
| `asset_bank.media.create` | An asset is created |
| `asset_bank.media.updated` | An asset is updated |
| `asset_bank.media.meta_updated` | An asset's metaproperty values change |
| `asset_bank.media.deleted` | An asset is deleted |
| `asset_bank.media.archived` | An asset is archived |
| `asset_bank.media.pre_archived` | An asset is approaching archival (lead time set by `preArchivedNotificationDays`) |
| `workflow.job.create` | A workflow job is created |
| `antivirus.scan.failed` | An antivirus scan fails (only when `antivirusEnabled` is set) |

## Steps

1. **List what already exists.** `GET /v7/webhooks/public/api/subscriptions`
   (documented at `https://api.bynder.com/reference/getwebhookconfigurations`),
   or `RetrieveaWebhookConfiguration` for a single subscription by id.
   Requires scope `webhooks.config:read` **and** the
   `View Webhooks configurations` security role.

2. **Create the subscription.** `CreateaWebhookConfiguration` with `name`,
   `endpoint` (your HTTPS receiver) and `events` (an array of the names above).
   Set `preArchivedNotificationDays` if you subscribe to `pre_archived`, and
   `antivirusEnabled` if you subscribe to `antivirus.scan.failed`.
   Requires scope `webhooks.config:write` **and** the
   `Manage Webhooks configurations` security role.

3. **Confirm it.** The subscription carries a `confirmed` flag. A subscription
   that is not confirmed does not deliver.

4. **Amend.** `UpdateaWebhookConfiguration` (full replace) or
   `PatchaWebhookConfiguration` (partial). `DeleteaWebhookConfiguration` to remove.

## What Bynder does NOT publish — plan around it

- **No payload schema.** The body Bynder POSTs to your endpoint is not specified
  anywhere. Write a tolerant receiver: accept unknown fields, key off the event
  name, and re-read the asset through `GET /api/v4/media/{id}` rather than
  trusting the payload to be complete.
- **No signature scheme.** There is no documented HMAC or signing header, so you
  cannot cryptographically authenticate an inbound Bynder webhook. Mitigate with a
  long unguessable path on your receiver endpoint and treat every event as a hint
  to re-read, never as an authenticated instruction.
- **No published source IP ranges** to allowlist.
- **No retry or delivery-guarantee policy.** Treat delivery as at-most-once and
  reconcile periodically with a list call.
