# Upstream Partner Contract Review — Shamba Direct API

Reviewed from the uploaded `Group 14 - openapi.yaml` against the Week 4 OpenAPI requirements (precise request/response types, required fields, realistic examples, and clear error cases).

This is a consumer-side review only. The source contract belongs to Shamba Direct; proposed contract changes should be agreed with that team before their shared `openapi.yaml` is changed.

## High-priority ambiguities and corrections

### 1. Invalid product status is documented as a server error
- **Location:** `ProductInput.status`
- **Current contract:** says any status outside `pending_review | active | sold_out` returns `500`.
- **Suggested correction:** return/document `400 Bad Request` for an invalid client-supplied enum. A 500 should mean an unexpected server/database failure.
- **Partner confirmation:** is this behavior implemented, or is the 500 description a mistake?

### 2. PUT semantics conflict with partial-update schemas
- **Locations:** `PUT /api/products/{id}` using `ProductPatchInput`; `PUT /api/headquarters/{id}` using `HeadquartersInput` with `requestBody.required: false`.
- **Current contract:** product PUT says any subset is accepted and omitted fields remain unchanged; headquarters PUT allows the body to be omitted while its schema requires `regionName` and `county`.
- **Suggested correction:** decide whether these operations are partial updates or full replacements. If partial, document PATCH (or explicitly document the partial-PUT behavior) and reject an empty/missing body with 400. If full replacement, require all replacement fields.

### 3. The rating average has inconsistent types
- **Location:** `GET /api/ratings?farmerId=...`
- **Current contract:** `averageRating` is a string such as `"4.5"`, but numeric `0` when there are no ratings.
- **Suggested correction:** return a number consistently (for example `4.5` and `0`) or a string consistently, and declare one schema/type. Consumers should not need to branch on whether ratings exist just to parse the value.

### 4. POST order response disagrees with the Order resource
- **Location:** `POST /api/orders`
- **Current contract:** the create response returns numeric `totalPrice`; the `Order` schema represents `total_price` as a decimal string (for example `"2250.00"`).
- **Suggested correction:** choose one response field name and type for the create response and order representation, or clearly document why the two representations intentionally differ.

### 5. Error response shapes are inconsistent
- **Locations:** global error conventions, `GET /api/test-db` 500, and shared `ServerError`.
- **Current contract:** says every failed request returns a single `error` string, but the database-check 500 response additionally includes `details`. The description also says malformed requests use the same error shape.
- **Suggested correction:** standardize errors to the shared `Error` schema, or explicitly document endpoint-specific exceptions and define their schemas. Avoid exposing raw database/credential details in public responses.

### 6. DELETE success responses differ from the lab handout's expected pattern
- **Locations:** product, order, rating, enquiry, contact, headquarters, market-price, and user DELETE operations.
- **Current contract:** documents `200` plus a JSON message.
- **Week 6 handout:** says successful DELETE should return `204 No Content`.
- **Suggested correction:** confirm the actual implementation and course expectation with the partner/instructor. If following the handout, change implementation and contract to 204 with no response body; otherwise document the deliberate deviation and keep implementation/spec consistent.

### 7. GET product has a write side effect
- **Location:** `GET /api/products/{id}`
- **Current contract:** says reading a product increments its view count.
- **Concern:** GET is expected to be safe; repeated retries, crawlers, caches, and prefetching can increment the counter unexpectedly.
- **Suggested correction:** count views through a dedicated POST endpoint or an explicit tracking action. If this behavior must remain, document its consequences for consumers and tests.

### 8. User profile shape is too vague for an integration contract
- **Location:** `User.profile`
- **Current contract:** `additionalProperties: true` with a description listing farmer and buyer fields.
- **Suggested correction:** define concrete farmer and buyer profile schemas (with `oneOf`/discriminator or another explicit shape), and specify nullable/optional fields. This lets a consumer validate actual responses instead of accepting any object.

### 9. Registration requirements depend on role but are not expressed
- **Location:** `RegisterInput`
- **Current contract:** only `role`, `fullName`, `phoneNumber`, and `password` are required; farmer-specific and buyer-specific fields are all optional.
- **Suggested correction:** document which extra fields are required for each role, using `oneOf` with separate farmer/buyer request schemas if the API enforces different requirements.

## Three questions to send to the partner

1. For `ProductInput.status`, should an invalid enum return 400 rather than the currently documented 500?
2. Should `averageRating` and `totalPrice` use consistent numeric types and field naming across their response shapes?
3. Are product/headquarters PUT operations partial updates, and should successful DELETE operations follow the Week 6 handout's 204/no-body convention?

## Verification limits

This review checks the uploaded OpenAPI document and the supplied course handouts. I have not run Shamba Direct's server or verified its actual responses. Before treating any suggested change as final, compare it with their implementation and run requests in Swagger UI as the Week 5 handout requires.
