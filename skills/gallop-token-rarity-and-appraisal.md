---
name: Gallop token rarity and appraisal
description: For a specific NFT, fetch its collection tokens, compute rarity, and get an appraisal/liquidation estimate.
api: openapi/gallop-analytics-openapi.json
operations: [getEthTokens, getEthRarity, getEthTokenAppraisal]
---

# Gallop token rarity and appraisal

Evaluate a single Ethereum NFT — its rarity within the collection and an estimated appraisal/liquidation value — using Gallop's Data, Analytics and Insights APIs.

## Auth & conventions
- Send `x-api-key: <API_KEY>` on every request.
- POST JSON to `https://api.prod.gallop.run/v1`; 5 req/s; `{ status, response }` envelope.

## Steps
1. **Tokens** — `getEthTokens` with `collection_address` to enumerate tokens and confirm the `token_id`.
2. **Rarity** — `getEthRarity` with `collection_address` for per-token rarity across the collection.
3. **Appraisal** — `getEthTokenAppraisal` with `collection_address` and `token_id`(s) for appraisal and liquidation estimates. Pass `horizon` + `frequency` to get forecasts instead of nowcasts.

## Notes
- Appraisal output is an analytical estimate, **not** individualized financial advice.
- `400` = malformed request (check `token_id` / `collection_address`); `403` = invalid API key. See `errors/gallop-problem-types.yml`.
