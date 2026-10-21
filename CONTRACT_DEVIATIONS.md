# Contract Deviations and Verification Notes

This file records known differences and clarifications between the FundiLink API implementation, its OpenAPI contract, and the lab expectations. Update it whenever a contract change is agreed with the downstream consumer.

## Current FundiLink contract clarifications

- Contract-facing routes are under `/api/jobs` and `/api/applications`; the API server defaults to port 3001.
- `GET /api/applications/{applicationId}/subscribe` currently sends a single Server-Sent Event containing the current status and then closes the response. It is **not** a persistent real-time subscription. This limitation is now stated in `openapi.yaml` and `ENDPOINT_LIST.md`. Confirm with SettleIn whether a persistent stream is required.
- Conflict responses (409) for unavailable/duplicate applications and invalid application state now document the JSON `Error` schema.
- Unmatched URLs return JSON 404 responses with a `message` field, matching the project's general error envelope.
- Browser compatibility routes (`/users`, `/jobs`, and `/applications`) remain available alongside the partner-facing `/api/*` routes.

## Upstream partner contract review

The uploaded Group 14 Shamba Direct contract has a separate review in `UPSTREAM_PARTNER_CONTRACT_REVIEW.md`. It identifies ambiguities around invalid enum status codes, PUT semantics, inconsistent numeric types, error envelopes, DELETE status codes, GET side effects, and role-dependent profile schemas. These are questions for the partner to confirm, not changes made to their API.

## Verification status

Automated Jest/Supertest tests are run by GitHub Actions on pushes. See the [Actions page](https://github.com/AringoA/FundiLinksProject/actions) for the latest run; do not infer success from an earlier commit's run. Run `npm install` and `npm test` locally before submission if possible.

Partner testing remains pending until SettleIn's independently written tests are actually executed against a running FundiLink API and the results are recorded in `PARTNER_TEST_RESULTS.md`. Do not claim partner testing passed without that evidence.
