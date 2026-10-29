# Bynder

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Bynder is a cloud-based digital asset management (DAM) platform used to store, organize, distribute and analyze brand and marketing assets. Its REST API is not one service but a federation of them behind each customer's own portal domain: the /api/v4 asset bank (assets, collections, metaproperties, brands, tags, smart filters, users and security profiles), an /api/1 taxonomy and content-access layer, /v6 OAuth 2.0 authorization, /v7 upload, webhooks and antivirus services, /api/workflow campaigns and jobs, and /api/store Brandstore ordering. Bynder publishes 34 OpenAPI 3.1 definitions covering 156 operations through its own API registry, a dated changelog, a documentation llms.txt, first-party SDKs for JavaScript, Python, PHP, Java and C#, and an embeddable asset-picker component. Authentication is OAuth 2.0 with JWT bearer tokens, layered on top of named security roles that gate operations independently of scope.

**Areas:** Digital Asset Management · Brand Management · Content Management · Marketing · Asset Workflow · Metadata · Content Operations · Media · Analytics

## Bynder on APIs.io

Everything profiled for Bynder is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/bynder/](https://apis.io/providers/bynder/)** — or go straight to one of the APIs or properties below.

### APIs (76)

- [Bynder Access rights API](https://apis.io/apis/bynder/bynder-access-rights-api/) — The Access rights API from Bynder — 1 operation(s) for access rights.
- [Bynder Account API](https://apis.io/apis/bynder/bynder-account-api/) — The Account API from Bynder — 2 operation(s) for account.
- [Bynder Asset Usage API](https://apis.io/apis/bynder/bynder-asset-usage-api/) — These calls allow you to keep track of assets being exported from Bynder and imported into a third party application. In order to get started or find an…
- [Bynder Asset Usage Sync API](https://apis.io/apis/bynder/bynder-asset-usage-sync-api/) — This alternative API call allows you to sync all your usage from a single integration. * A usage will be created when there is no existing usage on the…
- [Bynder Asset Usage V1 API](https://apis.io/apis/bynder/bynder-asset-usage-v1-api/) — These endpoints return information related to the specific event. You can enrich these events with specific data about the asset or the user by making use…
- [Bynder Asset Usage V2 API](https://apis.io/apis/bynder/bynder-asset-usage-v2-api/) — These endpoints return information related to the specific event. You can enrich these events with specific data about the asset or the user by making use…
- [Bynder Authorize endpoint API](https://apis.io/apis/bynder/bynder-authorize-endpoint-api/) — When using the Authorization Code grant, redirect the user to the [Authorize application](#reference/oauth-2.0/authorize-endpoint/authorize-application)…
- [Bynder Automation Workflow Actions API](https://apis.io/apis/bynder/bynder-automation-workflow-actions-api/) — The Automation Workflow Actions API from Bynder — 1 operation(s) for automation workflow actions.
- [Bynder Automation Workflow Conditions API](https://apis.io/apis/bynder/bynder-automation-workflow-conditions-api/) — The Automation Workflow Conditions API from Bynder — 1 operation(s) for automation workflow conditions.
- [Bynder Automation Workflow Rules API](https://apis.io/apis/bynder/bynder-automation-workflow-rules-api/) — The Automation Workflow Rules API from Bynder — 3 operation(s) for automation workflow rules.
- [Bynder Automation Workflow Triggers API](https://apis.io/apis/bynder/bynder-automation-workflow-triggers-api/) — The Automation Workflow Triggers API from Bynder — 1 operation(s) for automation workflow triggers.
- [Bynder Brands API](https://apis.io/apis/bynder/bynder-brands-api/) — The Brands API from Bynder — 1 operation(s) for brands.
- [Bynder Campaign jobs API](https://apis.io/apis/bynder/bynder-campaign-jobs-api/) — The Campaign jobs API from Bynder — 1 operation(s) for campaign jobs.
- [Bynder Campaigns API](https://apis.io/apis/bynder/bynder-campaigns-api/) — The Campaigns API from Bynder — 2 operation(s) for campaigns.
- [Bynder Collection Usage API](https://apis.io/apis/bynder/bynder-collection-usage-api/) — These endpoints return information related to the specific event. You can enrich these events with specific data about the collection or the user by making…
- [Bynder Collections API](https://apis.io/apis/bynder/bynder-collections-api/) — The Collections API from Bynder — 1 operation(s) for collections.
- [Bynder Collections assets API](https://apis.io/apis/bynder/bynder-collections-assets-api/) — The Collections assets API from Bynder — 1 operation(s) for collections assets.
- [Bynder Collections ID API](https://apis.io/apis/bynder/bynder-collections-id-api/) — The Collections ID API from Bynder — 1 operation(s) for collections id.
- [Bynder Configurations API](https://apis.io/apis/bynder/bynder-configurations-api/) — The Configurations API from Bynder — 1 operation(s) for configurations.
- [Bynder Create metaproperty option dependency group API](https://apis.io/apis/bynder/bynder-create-metaproperty-option-dependency-group-api/) — The Create metaproperty option dependency group API from Bynder — 1 operation(s) for create metaproperty option dependency group.
- [Bynder Current User API](https://apis.io/apis/bynder/bynder-current-user-api/) — Retrieve information about the currently authenticated user without needing to know their user ID.
- [Bynder Derivative Presets API](https://apis.io/apis/bynder/bynder-derivative-presets-api/) — The Derivative Presets API from Bynder — 2 operation(s) for derivative presets.
- [Bynder Document API](https://apis.io/apis/bynder/bynder-document-api/) — The Document API from Bynder — 1 operation(s) for document.
- [Bynder File upload API](https://apis.io/apis/bynder/bynder-file-upload-api/) — The File upload API from Bynder — 1 operation(s) for file upload.
- [Bynder Finish API](https://apis.io/apis/bynder/bynder-finish-api/) — The Finish API from Bynder — 1 operation(s) for finish.
- [Bynder Groups API](https://apis.io/apis/bynder/bynder-groups-api/) — Manage and retrieve groups within your Bynder account. Requires the **GROUPMANAGEMENT** security role.
- [Bynder Historical Data API](https://apis.io/apis/bynder/bynder-historical-data-api/) — This endpoint provides historical Analytics data beyond the 12 month retention period that applies to the Analytics API endpoints. **Note:** This data isn't…
- [Bynder Job media API](https://apis.io/apis/bynder/bynder-job-media-api/) — The Job media API from Bynder — 1 operation(s) for job media.
- [Bynder Job stages API](https://apis.io/apis/bynder/bynder-job-stages-api/) — The Job stages API from Bynder — 1 operation(s) for job stages.
- [Bynder Jobs API](https://apis.io/apis/bynder/bynder-jobs-api/) — The Jobs API from Bynder — 2 operation(s) for jobs.
- [Bynder Manage option dependency in dependency group API](https://apis.io/apis/bynder/bynder-manage-option-dependency-in-dependency-group-api/) — The Manage option dependency in dependency group API from Bynder — 1 operation(s) for manage option dependency in dependency group.
- [Bynder Manage ungrouped metaproperty option dependencies API](https://apis.io/apis/bynder/bynder-manage-ungrouped-metaproperty-option-dependencies-api/) — The Manage ungrouped metaproperty option dependencies API from Bynder — 1 operation(s) for manage ungrouped metaproperty option dependencies.
- [Bynder Media API](https://apis.io/apis/bynder/bynder-media-api/) — The Media API from Bynder — 3 operation(s) for media.
- [Bynder Media download API](https://apis.io/apis/bynder/bynder-media-download-api/) — The Media download API from Bynder — 3 operation(s) for media download.
- [Bynder Media ID API](https://apis.io/apis/bynder/bynder-media-id-api/) — The Media ID API from Bynder — 1 operation(s) for media id.
- [Bynder Media options API](https://apis.io/apis/bynder/bynder-media-options-api/) — The Media options API from Bynder — 1 operation(s) for media options.
- [Bynder Metaproperties API](https://apis.io/apis/bynder/bynder-metaproperties-api/) — The Metaproperties API from Bynder — 4 operation(s) for metaproperties.
- [Bynder Metaproperty operations API](https://apis.io/apis/bynder/bynder-metaproperty-operations-api/) — The Metaproperty operations API from Bynder — 1 operation(s) for metaproperty operations.
- [Bynder Metaproperty options operations API](https://apis.io/apis/bynder/bynder-metaproperty-options-operations-api/) — The Metaproperty options operations API from Bynder — 2 operation(s) for metaproperty options operations.
- [Bynder Options API](https://apis.io/apis/bynder/bynder-options-api/) — The Options API from Bynder — 4 operation(s) for options.
- [Bynder Options V1 API](https://apis.io/apis/bynder/bynder-options-v1-api/) — The Options V1 API from Bynder — 1 operation(s) for options v1.
- [Bynder Orders API](https://apis.io/apis/bynder/bynder-orders-api/) — The Orders API from Bynder — 4 operation(s) for orders.
- [Bynder Presets API](https://apis.io/apis/bynder/bynder-presets-api/) — The Presets API from Bynder — 1 operation(s) for presets.
- [Bynder Profiles API](https://apis.io/apis/bynder/bynder-profiles-api/) — To determine the security profile for your user you can compare the security profile id with the profileId retrieved from either the Retrieve specific user…
- [Bynder Public links API](https://apis.io/apis/bynder/bynder-public-links-api/) — The Public links API from Bynder — 1 operation(s) for public links.
- [Bynder Quarantine API](https://apis.io/apis/bynder/bynder-quarantine-api/) — The Quarantine API from Bynder — 3 operation(s) for quarantine.
- [Bynder Reporting API](https://apis.io/apis/bynder/bynder-reporting-api/) — These endpoints provide reporting capabilities for assets of the DAM, making it easier to build your own customised reports.
- [Bynder Retrieve all metaproperty option dependencies for a metaproperty API](https://apis.io/apis/bynder/bynder-retrieve-all-metaproperty-option-dependencies-for-a-metaproperty-api/) — The Retrieve all metaproperty option dependencies for a metaproperty API from Bynder — 1 operation(s) for retrieve all metaproperty option dependencies for…
- [Bynder Retrieve all metaproperty option dependencies globally API](https://apis.io/apis/bynder/bynder-retrieve-all-metaproperty-option-dependencies-globally-api/) — The Retrieve all metaproperty option dependencies globally API from Bynder — 1 operation(s) for retrieve all metaproperty option dependencies globally.
- [Bynder Retrieve options a metaproperty option depends on API](https://apis.io/apis/bynder/bynder-retrieve-options-a-metaproperty-option-depends-on-api/) — The Retrieve options a metaproperty option depends on API from Bynder — 1 operation(s) for retrieve options a metaproperty option depends on.
- [Bynder Scopes API](https://apis.io/apis/bynder/bynder-scopes-api/) — The Scopes API from Bynder — 1 operation(s) for scopes.
- [Bynder Search API](https://apis.io/apis/bynder/bynder-search-api/) — The Search API from Bynder — 1 operation(s) for search.
- [Bynder Search Usage API](https://apis.io/apis/bynder/bynder-search-usage-api/) — These endpoints return information related to the specific event. You can enrich these events with specific data about the asset or the user by making use…
- [Bynder Share collection API](https://apis.io/apis/bynder/bynder-share-collection-api/) — The Share collection API from Bynder — 1 operation(s) for share collection.
- [Bynder Smartfilters API](https://apis.io/apis/bynder/bynder-smartfilters-api/) — The Smartfilters API from Bynder — 1 operation(s) for smartfilters.
- [Bynder Specific metaproperty operations API](https://apis.io/apis/bynder/bynder-specific-metaproperty-operations-api/) — The Specific metaproperty operations API from Bynder — 1 operation(s) for specific metaproperty operations.
- [Bynder Specific metaproperty option dependency group operations API](https://apis.io/apis/bynder/bynder-specific-metaproperty-option-dependency-group-operations-api/) — The Specific metaproperty option dependency group operations API from Bynder — 1 operation(s) for specific metaproperty option dependency group operations.
- [Bynder Specific metaproperty option operations API](https://apis.io/apis/bynder/bynder-specific-metaproperty-option-operations-api/) — The Specific metaproperty option operations API from Bynder — 1 operation(s) for specific metaproperty option operations.
- [Bynder Step 1 API](https://apis.io/apis/bynder/bynder-step-1-api/) — This endpoint prepares the upload of a file in chunks. It returns a file ID that will be used in subsequent steps to upload the file chunks and finalize the…
- [Bynder Step 2 API](https://apis.io/apis/bynder/bynder-step-2-api/) — This endpoint uploads a chunk of the file. You need to provide the file ID obtained from the prepare upload step and the chunk number (starting from 0). The…
- [Bynder Step 3 API](https://apis.io/apis/bynder/bynder-step-3-api/) — This endpoint finalizes the upload after all chunks have been uploaded. You need to provide the file ID and details about the file, including its name,…
- [Bynder Token endpoint API](https://apis.io/apis/bynder/bynder-token-endpoint-api/) — Use the token endpoint to retrieve a access token which can be used to authorize API requests. Depending on the type of grant, different fields are required…
- [Bynder Transform API](https://apis.io/apis/bynder/bynder-transform-api/) — The Transform API from Bynder — 1 operation(s) for transform.
- [Bynder Trash API](https://apis.io/apis/bynder/bynder-trash-api/) — The Trash API from Bynder — 1 operation(s) for trash.
- [Bynder User Usage API](https://apis.io/apis/bynder/bynder-user-usage-api/) — These endpoints return information related to the specific event. You can enrich these events with specific data about the asset or the user by making use…
- [Bynder Users API](https://apis.io/apis/bynder/bynder-users-api/) — Manage users within your Bynder account. You can create, retrieve, update, and delete users as needed.
- [Bynder Users ID API](https://apis.io/apis/bynder/bynder-users-id-api/) — Manage specific users by their ID. This includes retrieving, updating, and deleting user information based on the user ID.
- [Bynder Step 1 Get closest AmazonS3 upload endpoint API](https://apis.io/apis/bynder/bynder-step-1-get-closest-amazons3-upload-endpoint-api/) — This endpoint prepares the upload of a file in chunks. It returns a file ID that will be used in subsequent steps to upload the file chunks and finalize the…
- [Bynder Step 2 Initialise upload API](https://apis.io/apis/bynder/bynder-step-2-initialise-upload-api/) — This endpoint uploads a chunk of the file. You need to provide the file ID obtained from the prepare upload step and the chunk number (starting from 0). The…
- [Bynder Step 3A Upload file in chunks API](https://apis.io/apis/bynder/bynder-step-3a-upload-file-in-chunks-api/) — This endpoint finalizes the upload after all chunks have been uploaded. You need to provide the file ID and details about the file, including its name,…
- [Bynder Step 3B Register uploaded chunk API](https://apis.io/apis/bynder/bynder-step-3b-register-uploaded-chunk-api/) — This endpoint finalizes the upload after all chunks have been uploaded. You need to provide the file ID and details about the file, including its name,…
- [Bynder Step 4 EITHER Finalise uploaded file API](https://apis.io/apis/bynder/bynder-step-4-either-finalise-uploaded-file-api/) — The Step 4 EITHER Finalise uploaded file API from Bynder — 1 operation(s) for step 4 either finalise uploaded file.
- [Bynder Step 4 OR Finalize and save an additional uploaded file as a new asset. API](https://apis.io/apis/bynder/bynder-step-4-or-finalize-and-save-an-additional-uploaded-file-as-a-new-asset-api/) — The Step 4 OR Finalize and save an additional uploaded file as a new asset. API from Bynder — 1 operation(s) for step 4 or finalize and save an additional…
- [Bynder Step 5 Poll for processing status API](https://apis.io/apis/bynder/bynder-step-5-poll-for-processing-status-api/) — This endpoint allows you to check the processing status of a finalized upload. It should be called repeatedly until the response indicates that the…
- [Bynder Step 6 EITHER Save as a new asset API](https://apis.io/apis/bynder/bynder-step-6-either-save-as-a-new-asset-api/) — This endpoint finalizes the upload after all chunks have been uploaded. You need to provide the file ID and details about the file, including its name,…
- [Bynder Step 6 OR Save uploaded file to existing asset API](https://apis.io/apis/bynder/bynder-step-6-or-save-uploaded-file-to-existing-asset-api/) — The Step 6 OR Save uploaded file to existing asset API from Bynder — 1 operation(s) for step 6 or save uploaded file to existing asset.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Bynder Webhooks](https://apis.io/asyncapis/bynder/bynder-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [bynder-mcp.yml](https://apis.io/servers/bynder/bynder-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Bynder Agentic Access](https://apis.io/agentic-access/bynder/bynder-agentic-access/)

#### Collections (35)

Postman and Open Collection request collections.

- [Bynder API](https://apis.io/collections/bynder/open-bynder/)
- [Access Rights and Optiops API](https://apis.io/collections/bynder/open-bynder-access-rights-and-options-v4/)
- [Access Rights API](https://apis.io/collections/bynder/open-bynder-access-rights-v4/)
- [Account API](https://apis.io/collections/bynder/open-bynder-account-v4/)
- [Analytics API](https://apis.io/collections/bynder/open-bynder-analytics/)
- [Antivirus API](https://apis.io/collections/bynder/open-bynder-antivirus/)
- [Download API](https://apis.io/collections/bynder/open-bynder-asset-download/)
- [Upload Assets API](https://apis.io/collections/bynder/open-bynder-asset-upload/)
- [Asset Usage API](https://apis.io/collections/bynder/open-bynder-asset-usage-v4/)
- [Asset Management API](https://apis.io/collections/bynder/open-bynder-asset-v4/)
- [Automation Workflow API](https://apis.io/collections/bynder/open-bynder-automation-workflow-svc/)
- [Adaptive Video Streaming API](https://apis.io/collections/bynder/open-bynder-avs/)
- [Brands](https://apis.io/collections/bynder/open-bynder-brands-v4/)
- [Brandstore API](https://apis.io/collections/bynder/open-bynder-brandstore/)
- [Collections API](https://apis.io/collections/bynder/open-bynder-collections-v4/)
- [Dynamic Asset Transformations API](https://apis.io/collections/bynder/open-bynder-dat/)
- [Derivative Presets API](https://apis.io/collections/bynder/open-bynder-derivative-presets/)
- [Groups](https://apis.io/collections/bynder/open-bynder-groups-v4/)
- [Metaproperty Operations](https://apis.io/collections/bynder/open-bynder-metaproperty-v4/)
- [Modern Stack File Upload](https://apis.io/collections/bynder/open-bynder-modern-stack-upload/)
- [OAuth 2.0](https://apis.io/collections/bynder/open-bynder-oauth2/)
- [Metaproperty Options API](https://apis.io/collections/bynder/open-bynder-options-v4/)
- [Product Layer Metaproperties API](https://apis.io/collections/bynder/open-bynder-product-layer-v4/)
- [Security Roles](https://apis.io/collections/bynder/open-bynder-securityroles-v4/)
- [Similar Assets Search API](https://apis.io/collections/bynder/open-bynder-similar-assets/)
- …and 10 more published on APIs.io

#### Overlays (34)

OpenAPI overlays, including conversational phrasing for each operation.

- [Bynder Access Rights And Options V4 Overlay](https://apis.io/overlays/bynder/bynder-access-rights-and-options-v4-overlay/)
- [Bynder Access Rights V4 Overlay](https://apis.io/overlays/bynder/bynder-access-rights-v4-overlay/)
- [Bynder Account V4 Overlay](https://apis.io/overlays/bynder/bynder-account-v4-overlay/)
- [Bynder Analytics Overlay](https://apis.io/overlays/bynder/bynder-analytics-overlay/)
- [Bynder Antivirus Overlay](https://apis.io/overlays/bynder/bynder-antivirus-overlay/)
- [Bynder Asset Download Overlay](https://apis.io/overlays/bynder/bynder-asset-download-overlay/)
- [Bynder Asset Upload Overlay](https://apis.io/overlays/bynder/bynder-asset-upload-overlay/)
- [Bynder Asset Usage V4 Overlay](https://apis.io/overlays/bynder/bynder-asset-usage-v4-overlay/)
- [Bynder Asset V4 Overlay](https://apis.io/overlays/bynder/bynder-asset-v4-overlay/)
- [Bynder Automation Workflow Svc Overlay](https://apis.io/overlays/bynder/bynder-automation-workflow-svc-overlay/)
- [Bynder Avs Overlay](https://apis.io/overlays/bynder/bynder-avs-overlay/)
- [Bynder Brands V4 Overlay](https://apis.io/overlays/bynder/bynder-brands-v4-overlay/)
- [Bynder Brandstore Overlay](https://apis.io/overlays/bynder/bynder-brandstore-overlay/)
- [Bynder Collections V4 Overlay](https://apis.io/overlays/bynder/bynder-collections-v4-overlay/)
- [Bynder Dat Overlay](https://apis.io/overlays/bynder/bynder-dat-overlay/)
- [Bynder Derivative Presets Overlay](https://apis.io/overlays/bynder/bynder-derivative-presets-overlay/)
- [Bynder Groups V4 Overlay](https://apis.io/overlays/bynder/bynder-groups-v4-overlay/)
- [Bynder Metaproperty V4 Overlay](https://apis.io/overlays/bynder/bynder-metaproperty-v4-overlay/)
- [Bynder Modern Stack Upload Overlay](https://apis.io/overlays/bynder/bynder-modern-stack-upload-overlay/)
- [Bynder Oauth2 Overlay](https://apis.io/overlays/bynder/bynder-oauth2-overlay/)
- [Bynder Options V4 Overlay](https://apis.io/overlays/bynder/bynder-options-v4-overlay/)
- [Bynder Product Layer V4 Overlay](https://apis.io/overlays/bynder/bynder-product-layer-v4-overlay/)
- [Bynder Securityroles V4 Overlay](https://apis.io/overlays/bynder/bynder-securityroles-v4-overlay/)
- [Bynder Similar Assets Overlay](https://apis.io/overlays/bynder/bynder-similar-assets-overlay/)
- [Bynder Smartfilter V4 Overlay](https://apis.io/overlays/bynder/bynder-smartfilter-v4-overlay/)
- …and 9 more published on APIs.io

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Bynder Authentication](https://apis.io/security/bynder/bynder-authentication/)
- [Bynder Domain Security](https://apis.io/security/bynder/bynder-domain-security/)
- [Bynder Trust Center](https://apis.io/security/bynder/bynder-trust-center/)
- [Bynder Vulnerability Disclosure](https://apis.io/security/bynder/bynder-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Bynder Scopes](https://apis.io/scopes/bynder/bynder-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Bynder Plans Pricing](https://apis.io/plans/bynder/bynder-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Bynder Rate Limits](https://apis.io/rate-limits/bynder/bynder-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.bynder.com)
- [Documentation](https://api.bynder.com/docs/getting-started)
- [Getting started](https://api.bynder.com/docs/getting-started)
- [API reference](https://api.bynder.com/reference)
- [Pricing](https://www.bynder.com/en/pricing/)
- [Support](https://support.bynder.com)
- [Blog](https://www.bynder.com/en/blog/rss.xml)
- [Security](https://www.bynder.com/en/legal/responsible-disclosure-policy/)
- [Compliance](https://trust.bynder.com/)
- [Terms of service](https://www.bynder.com/en/legal/terms-of-use/)
- [Privacy policy](https://www.bynder.com/en/legal/privacy-policy/)
- [GitHub](https://github.com/Bynder)
- [Status](https://status.bynder.com)

## API Evangelist rating

**Kin Score 61.1** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 59.8 |
| Contract governance | 18.2 |
| Operational transparency | 73.7 |
| Developer ergonomics | 66.1 |
| Access clarity | 47.4 |

**Agent readiness 38.6** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | documented (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | mostly |

**Regulatory alignment 45.1** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/bynder/](https://apis.io/providers/bynder/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Bynder: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/bynder/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
