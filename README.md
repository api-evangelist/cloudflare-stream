# Cloudflare Stream (cloudflare-stream)

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

Cloudflare Stream is the video streaming, hosting, and live-video product from Cloudflare - a single REST API for uploading, storing, encoding, and delivering on-demand and live video across Cloudflare's global network. It handles direct and TUS resumable uploads, copy-from-URL ingest, live inputs over RTMPS and SRT (with simulcast outputs and a WebRTC/WHIP/WHEP live beta), a built-in adaptive-bitrate player with HLS/DASH manifests, AI-generated and uploaded captions, signed-URL access control, per-account webhooks, and viewing analytics.

This entry documents the **Cloudflare Stream product specifically**, not the broader Cloudflare platform (which is catalogued separately under `cloudflare`).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/cloudflare-stream/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/cloudflare-stream/refs/heads/main/apis.yml)

## Access Model

Cloudflare Stream is a proprietary, fully managed Cloudflare service. It is **not open source and is not self-hostable** - the service runs only on Cloudflare's network and requires a Cloudflare account.

- **Base URL:** `https://api.cloudflare.com/client/v4`, with all operations scoped to an account under `/accounts/{account_id}/stream`.
- **Authentication:** a Cloudflare **API token** passed as an `Authorization: Bearer <token>` header. Tokens are created in the Cloudflare dashboard and scoped with Stream permissions.
- **Surface:** request/response REST over HTTPS. The only push mechanism is a single per-account **webhook** (outbound HTTP) that fires when a video finishes processing or errors. Video ingest and playback use streaming media protocols (RTMPS, SRT, HLS, DASH) and a WebRTC-based WHIP/WHEP live beta - there is **no documented client WebSocket API**.

## Pricing

Simple usage-based pricing with no per-request API fee:

- **Storage:** $5 per 1,000 minutes of video stored (prepaid, in increments).
- **Delivery:** $1 per 1,000 minutes of video delivered / watched (post-paid).

Encoding, the built-in player, and HLS/DASH delivery are included. Live and on-demand video share the same billing model - a live broadcast with no viewers costs nothing to deliver, but recordings count toward stored minutes. See [plans/cloudflare-stream-plans-pricing.yml](plans/cloudflare-stream-plans-pricing.yml).

## Tags

- Video
- Streaming
- Live Streaming
- Media
- Video Hosting
- Cloudflare

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Cloudflare Stream Videos API

Upload, store, encode, list, edit, and delete on-demand video. Supports direct uploads, TUS resumable uploads, copy-from-URL ingest, one-time direct creator uploads, video clipping, per-video audio tracks, and account storage usage - all under `/accounts/{account_id}/stream`.

- **Human URL:** [https://developers.cloudflare.com/api/resources/stream/](https://developers.cloudflare.com/api/resources/stream/)
- **Base URL:** `https://api.cloudflare.com/client/v4`

#### Tags

- Video
- Uploads
- On-Demand

#### Properties

- [Documentation](https://developers.cloudflare.com/stream/)
- [API Reference](https://developers.cloudflare.com/api/resources/stream/)
- [Getting Started](https://developers.cloudflare.com/stream/get-started/)
- [OpenAPI](openapi/cloudflare-stream-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cloudflare-stream.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudflare-stream.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cloudflare Stream Live Inputs API

Create and manage live inputs that receive broadcasts over RTMPS or SRT and deliver them live and as recordings. Manage simulcast outputs that restream one input to other RTMP or SRT destinations, under `/accounts/{account_id}/stream/live_inputs`.

- **Human URL:** [https://developers.cloudflare.com/api/resources/stream/subresources/live_inputs/](https://developers.cloudflare.com/api/resources/stream/subresources/live_inputs/)
- **Base URL:** `https://api.cloudflare.com/client/v4`

#### Tags

- Live Streaming
- RTMPS
- SRT

#### Properties

- [Documentation](https://developers.cloudflare.com/stream/stream-live/)
- [API Reference](https://developers.cloudflare.com/api/resources/stream/subresources/live_inputs/)
- [OpenAPI](openapi/cloudflare-stream-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cloudflare-stream.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudflare-stream.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cloudflare Stream Captions API

List, upload, AI-generate, retrieve (including WebVTT), and delete per-language captions and subtitles for a video, keyed by BCP 47 language tag, under `/accounts/{account_id}/stream/{identifier}/captions`.

- **Human URL:** [https://developers.cloudflare.com/api/resources/stream/subresources/captions/](https://developers.cloudflare.com/api/resources/stream/subresources/captions/)
- **Base URL:** `https://api.cloudflare.com/client/v4`

#### Tags

- Captions
- Subtitles
- Accessibility

#### Properties

- [Documentation](https://developers.cloudflare.com/stream/edit-videos/adding-captions/)
- [API Reference](https://developers.cloudflare.com/api/resources/stream/subresources/captions/)
- [OpenAPI](openapi/cloudflare-stream-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cloudflare-stream.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudflare-stream.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cloudflare Stream Signed URLs API

Restrict playback with signed URLs. Create and revoke RSA signing keys (up to 1,000 per account) under `/accounts/{account_id}/stream/keys`, and mint per-video signed tokens via `POST /accounts/{account_id}/stream/{identifier}/token` with configurable expiry and access rules.

- **Human URL:** [https://developers.cloudflare.com/stream/viewing-videos/securing-your-stream/](https://developers.cloudflare.com/stream/viewing-videos/securing-your-stream/)
- **Base URL:** `https://api.cloudflare.com/client/v4`

#### Tags

- Signed URLs
- Access Control
- Security

#### Properties

- [Documentation](https://developers.cloudflare.com/stream/viewing-videos/securing-your-stream/)
- [API Reference](https://developers.cloudflare.com/api/resources/stream/subresources/keys/)
- [OpenAPI](openapi/cloudflare-stream-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cloudflare-stream.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudflare-stream.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cloudflare Stream Webhooks API

Subscribe, view, and delete the single per-account webhook that Stream calls when a video finishes processing or enters an error state. Notifications are signed with a secret and carry `uid`, `readyToStream`, and `status` fields, under `/accounts/{account_id}/stream/webhook`.

- **Human URL:** [https://developers.cloudflare.com/stream/manage-video-library/using-webhooks/](https://developers.cloudflare.com/stream/manage-video-library/using-webhooks/)
- **Base URL:** `https://api.cloudflare.com/client/v4`

#### Tags

- Webhooks
- Events
- Notifications

#### Properties

- [Documentation](https://developers.cloudflare.com/stream/manage-video-library/using-webhooks/)
- [API Reference](https://developers.cloudflare.com/api/resources/stream/subresources/webhooks/)
- [OpenAPI](openapi/cloudflare-stream-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cloudflare-stream.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudflare-stream.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Cloudflare Stream Analytics API

Measure minutes viewed and stored. Read account video storage usage via `GET /accounts/{account_id}/stream/storage-usage`, and query rich viewing analytics (minutes viewed, by video, country, and time) through the Cloudflare GraphQL Analytics API stream datasets.

- **Human URL:** [https://developers.cloudflare.com/stream/getting-analytics/](https://developers.cloudflare.com/stream/getting-analytics/)
- **Base URL:** `https://api.cloudflare.com/client/v4`

#### Tags

- Analytics
- Reporting
- Usage

#### Properties

- [Documentation](https://developers.cloudflare.com/stream/getting-analytics/)
- [API Reference](https://developers.cloudflare.com/analytics/graphql-api/)
- [OpenAPI](openapi/cloudflare-stream-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/cloudflare-stream.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/cloudflare-stream.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/cloudflare)
- [Website](https://www.cloudflare.com/products/cloudflare-stream/)
- [Documentation](https://developers.cloudflare.com/stream/)
- [Plans](plans/cloudflare-stream-plans-pricing.yml)
- [Rate Limits](rate-limits/cloudflare-stream-rate-limits.yml)
- [Fin Ops](finops/cloudflare-stream-finops.yml)
- [GitHub Organization](https://github.com/cloudflare)
- [Pricing](https://developers.cloudflare.com/stream/pricing/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
