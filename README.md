# Cloudflare Stream (cloudflare-stream)

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
