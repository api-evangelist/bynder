---
name: Move a Bynder workflow job through its stages
description: >-
  Create a workflow job under a campaign, attach assets to it, read its stages,
  advance it, and finish it — the creative-review flow in Bynder Asset Workflow.
api: openapi/bynder-wf-jobs-v4-openapi.json
operations:
  - "GET /api/workflow/jobs"
  - "POST /api/workflow/jobs"
  - "GET /api/workflow/campaigns/{id}/jobs"
  - "GET /api/workflow/jobs/{id}"
  - "PUT /api/workflow/jobs/{id}"
  - "GET /api/workflow/jobs/{id}/stages"
  - "GET /api/workflow/jobs/{id}/media"
  - "POST /workflow-jobs/{id}/upload"
  - "PATCH /api/workflow/jobs/{id}/finish"
  - "DELETE /api/workflow/jobs/{id}"
generated: '2026-08-13'
method: generated
source: >-
  openapi/bynder-wf-jobs-v4-openapi.json and openapi/bynder-wf-campaigns-v4-openapi.json
---

# Move a Bynder workflow job through its stages

Asset Workflow is a separate service from the asset bank, on `/api/workflow/`,
with its own scopes and its own status page component ("Workflow API v5").

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

1. **Find the campaign.** `GET /api/workflow/campaigns`
   (scope `workflow.campaign:read`). Jobs live under a campaign.

2. **List existing jobs.** `GET /api/workflow/jobs`, or
   `GET /api/workflow/campaigns/{id}/jobs` for one campaign.
   Scope `workflow.job:read`.

3. **Create the job.** `POST /api/workflow/jobs` with the campaign, name, preset
   and assignees. Scope `workflow.job:write` plus the `JOBADD` security role.
   Read the available preset first with `GET /api/workflow/presets/job/{id}`
   (scope `workflow.preset:read`).

4. **Attach assets.** `POST /workflow-jobs/{id}/upload` to upload into the job,
   then `GET /api/workflow/jobs/{id}/media` to confirm.

5. **Read the stages.** `GET /api/workflow/jobs/{id}/stages` returns the stage
   list and where the job currently sits.

6. **Advance it.** `PUT /api/workflow/jobs/{id}` modifies the job, including
   `activeStage`. **Bynder restricted the accepted `activeStage` statuses in July
   2025** — read the current stage list from step 5 and only send a status that
   appears there. Sending an out-of-range status returns 409, not 400.

7. **Finish it.** `PATCH /api/workflow/jobs/{id}/finish`. Requires scope
   `workflow.job:approve` and the `JOBAPPROVE` role.

## Failure handling

- **409 Conflict** — "the job is not open (has been finished)" or the
  `activeStage.status` is not valid for this job's current position. Re-read the
  job and its stages; do **not** retry the same request, it will keep failing.
- **403** — the profile lacks `JOBADD`, `JOBEDIT`, `JOBAPPROVE` or `WORKFLOWADMIN`
  as appropriate.
- Errors on this service come back as `application/vnd.api+json`, unlike the asset
  bank's `application/json`. Do not assume one error shape across Bynder.
