---
name: Gallop wallet portfolio valuation
description: Value an Ethereum wallet's NFT portfolio and profile its trading behaviour — holdings, valuation, profit-and-loss, and activity labels.
api: openapi/gallop-data-openapi.json
operations: [getEthWalletNFTs, getEthWalletValuation, getEthWalletPnL, getEthWalletLabels]
---

# Gallop wallet portfolio valuation

Given an Ethereum `wallet_address`, produce a valued portfolio plus a behavioural profile using Gallop's Data, Insights and Analytics APIs.

## Auth & conventions
- Send `x-api-key: <API_KEY>` on every request.
- POST JSON to `https://api.prod.gallop.run/v1`; obey the 5 req/s limit; read data from the `response` field of the envelope.

## Steps
1. **Holdings** — `getEthWalletNFTs` with `wallet_address` to list every token (ERC-721 / ERC-1155) the wallet owns.
2. **Valuation** — `getEthWalletValuation` with `wallet_address` to value all owned tokens.
3. **Profit & loss** — `getEthWalletPnL` with `wallet_address` for realized/unrealized P&L across the wallet's NFT transactions.
4. **Behaviour labels** — `getEthWalletLabels` with `wallet_address` for volume / activity / wash-trading labels.

## Notes
- `getEthWalletLabels` thresholds (light/neutral/high, dormant/active, wash none/low/moderate/high) are quantile-based and can shift; treat them as relative, not absolute.
- Errors follow `errors/gallop-problem-types.yml` (`400` bad input, `403` bad key).
