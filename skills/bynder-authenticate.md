---
name: Authenticate against a Bynder portal
description: >-
  Obtain a Bynder OAuth 2.0 access token for a customer portal using either the
  authorization-code flow (acting as a user) or the client-credentials flow
  (acting as an integration), and discover which scopes the token actually got.
api: openapi/bynder-oauth2-openapi.json
operations:
  - "GET /v6/authentication/oauth2/auth"
  - "POST /v6/authentication/oauth2/token"
  - "GET /v6/authentication/oauth2/scopes"
generated: '2026-08-13'
method: generated
source: >-
  openapi/bynder-oauth2-openapi.json and https://api.bynder.com/docs/getting-started
---

# Authenticate against a Bynder portal

Every other Bynder skill starts here. Bynder supports exactly one authorization
protocol: OAuth 2.0 with a JWT bearer access token in the `Authorization` header.

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

## Choose the flow

| Situation | Flow | Endpoint |
|---|---|---|
| You act on behalf of a signed-in Bynder user | authorization code | `GET /v6/authentication/oauth2/auth` then `POST /v6/authentication/oauth2/token` |
| You act as a background integration with no user | client credentials | `POST /v6/authentication/oauth2/token` |
| Your access token expired | refresh token | `POST /v6/authentication/oauth2/token` with `grant_type=refresh_token` |

## Steps

1. **Authorization code only — send the user to the authorize endpoint.**
   `GET /v6/authentication/oauth2/auth` on the customer's portal host with
   `client_id`, `redirect_uri`, `response_type=code`, `scope` (space separated)
   and `state`. Bynder redirects back with `code`.
   Request the `offline` behaviour by including a refresh grant in your app
   registration if you need long-lived access.

2. **Exchange for a token.**
   `POST /v6/authentication/oauth2/token` with `grant_type=authorization_code`
   (plus `code` and `redirect_uri`) or `grant_type=client_credentials`.
   The response carries a JWT `access_token`.

3. **Check what you actually got.** Bynder grants the *intersection* of the scopes
   you asked for and the user's security profile — you can be issued fewer scopes
   than you requested, silently. Call
   `GET /v6/authentication/oauth2/scopes` to read the scope list and the user
   permissions each one requires, and compare it against what you need.

4. **Send it.** `Authorization: Bearer <access_token>` on every subsequent call.

5. **Refresh before expiry.** `POST /v6/authentication/oauth2/token` with
   `grant_type=refresh_token`. There is no token-introspection endpoint and no
   `/.well-known/oauth-authorization-server` document — you cannot discover the
   endpoints at runtime, they are the fixed paths above on the portal host.

## Scopes you will most likely need

`asset:read`, `asset:write`, `collection:read`, `collection:write`,
`meta.assetbank:read`, `meta.assetbank:write`, `current.user:read`.
The full 29-scope table with the operations each covers is in
`scopes/bynder-scopes.yml`.

## Failure handling

- **401** — token missing, malformed or expired. Refresh, then retry once.
- **403** — token is fine; the user's security profile lacks the required named
  role. Do not retry. Name the missing role to the caller.
