---
name: Gallop collection market snapshot
description: Pull a market snapshot for an NFT collection on Ethereum — supported collections, per-marketplace summary, floor price, and analytical summary.
api: openapi/gallop-data-openapi.json
operations: [getEthCollections, getEthMarketplaceData, getEthMarketplaceFloorPrice, getEthCollectionSummary]
---

# Gallop collection market snapshot

Assemble a market snapshot for one Ethereum NFT collection using Gallop's Data and Analytics APIs.

## Auth & conventions
- Send `x-api-key: <API_KEY>` on every request (see `authentication/gallop-authentication.yml`).
- All operations are **POST** with a JSON body against base URL `https://api.prod.gallop.run/v1`.
- Rate limit: **5 requests/second** per key. Responses use the `{ status, response }` envelope.
- Paginate with `page` and `page_size` (one of 50, 100, 500, 1000).

## Steps
1. **Resolve the collection** — `getEthCollections` with `collection_name` (or browse pages) to obtain the `collection_address`.
2. **Marketplace summary** — `getEthMarketplaceData` with the `collection_address` for per-marketplace volume/sales stats.
3. **Floor price** — `getEthMarketplaceFloorPrice` with the `collection_address` for the current floor by marketplace.
4. **Analytical summary** — `getEthCollectionSummary` with the `collection_address` for aggregate analytics (avg daily volume, latest floor, peaks/troughs).

## Notes
- On a `403`, the API key is missing/invalid; on a `400`, re-check `collection_address` and that `page_size` is an allowed enum value (see `errors/gallop-problem-types.yml`).
- Swap the `eth` path segment for `sol` / `pol` to run the same flow on Solana or Polygon where the equivalent operations exist.
