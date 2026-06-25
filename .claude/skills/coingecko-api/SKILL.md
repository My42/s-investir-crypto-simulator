---
name: coingecko-api
description: Use when fetching crypto market data — coin prices, market caps, historical charts, OHLC candlesticks, trending coins, exchanges, NFTs, or on-chain DEX/pool data — via the CoinGecko or GeckoTerminal API. Covers coin ID resolution, plan/auth setup, endpoints, and date-format gotchas.
---

# CoinGecko API

## Overview

Two APIs share one `CG-` key. **CoinGecko** = aggregated data for well-known assets. **GeckoTerminal** = on-chain DEX data for long-tail tokens and pools (append `/onchain` to the base URL).

Latest docs: https://docs.coingecko.com/

## Plans & Auth

Both Demo and Pro keys start with `CG-`, so the prefix is ambiguous. **Ask the user which plan they're on — never guess.** Then hard-code the matching base URL + header; do not write branching logic.

| Plan | Rate Limit | Base URL | Auth Header |
|---|---|---|---|
| **Demo** | 30 calls/min | `https://api.coingecko.com/api/v3` | `x-cg-demo-api-key: KEY` |
| **Pro (Paid)** | 250+ calls/min | `https://pro-api.coingecko.com/api/v3` | `x-cg-pro-api-key: KEY` |

Use header **or** query param — never both.

## Quick Start (Node.js, Demo key)

```typescript
const BASE_URL = "https://api.coingecko.com/api/v3";
const API_KEY = process.env.CG_API_KEY; // your CG-... key

const res = await fetch(`${BASE_URL}/simple/price?ids=bitcoin,ethereum&vs_currencies=usd`, {
  headers: { "x-cg-demo-api-key": API_KEY },
});
```

For Pro: swap base URL to `https://pro-api.coingecko.com/api/v3` and header to `x-cg-pro-api-key`.

## Resolve Coin IDs First

Never guess coin IDs — resolve them before any data call:

```
GET /search?query=solana          # IDs for coins, exchanges, categories, NFTs
GET /coins/list                   # full ID list
```

## Core Endpoints

| Use case | Endpoint |
|---|---|
| Live price | `GET /simple/price?ids=bitcoin,ethereum&vs_currencies=usd&include_market_cap=true&include_24hr_vol=true` |
| Market list (ranking, sparkline, ATH/ATL) | `GET /coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=true` |
| Coin detail | `GET /coins/bitcoin?localization=false&tickers=false&community_data=false&developer_data=false` |
| Historical chart | `GET /coins/bitcoin/market_chart?vs_currency=usd&days=30` |
| Historical range | `GET /coins/bitcoin/market_chart/range?vs_currency=usd&from=2024-01-01&to=2024-03-01` |
| OHLC candlesticks | `GET /coins/bitcoin/ohlc?vs_currency=usd&days=30` |
| Trending (24h) | `GET /search/trending` |
| Top gainers/losers | `GET /coins/top_gainers_losers?vs_currency=usd&duration=24h` |
| New coins | `GET /coins/list/new` |
| Categories | `GET /coins/categories` |
| Exchanges | `GET /exchanges` |
| NFT floor prices | `GET /nfts/{id}`, `GET /nfts/markets` |
| API health / usage | `GET /ping`, `GET /key` |

`market_chart` auto-granularity: 1d → 5-min, 2–90d → hourly, 90d+ → daily. Override with `interval=daily` or `interval=hourly`.

`simple/price` supports `ids`, `names`, or `symbols`. Add `include_last_updated_at=true` to detect stale prices.

## GeckoTerminal (On-Chain DEX) — append `/onchain`

Use for long-tail tokens, DEX-native tokens, pools, and on-chain trade data not on CoinGecko.

| Use case | Endpoint |
|---|---|
| Token price by contract | `GET /onchain/simple/networks/eth/token_price/0xdac17f958d2ee523a2206206994597c13d831ec7` |
| Pool data | `GET /onchain/networks/eth/pools/0x88e6a0c2ddd26feeb64f039a2c41296fcb3f5640` |
| Trending pools | `GET /onchain/networks/trending_pools` |
| New pools | `GET /onchain/networks/new_pools` |
| Pool screener (megafilter) | `GET /onchain/pools/megafilter?sort=pool_created_at_desc` |
| Token security / GT score | `GET /onchain/networks/eth/tokens/{address}/info` |
| Top holders | `GET /onchain/networks/eth/tokens/{address}/top_holders` |

Megafilter filters by FDV, liquidity, volume, pool age, buy/sell tax, honeypot checks, and more.

## Date/Time Formats (varies per endpoint — check before calling)

| Context | Format |
|---|---|
| Coin/Contract/Supply `from`/`to` | ISO `YYYY-MM-DD` |
| `GET /exchanges/{id}/volume_chart/range` `from`/`to` | UNIX timestamp (seconds) |
| `GET /coins/{id}/history` `date` | `DD-MM-YYYY` |
| GeckoTerminal `before_timestamp` | UNIX timestamp (seconds) |

For "now", "today", "this week", always use the actual current system date — never infer from training data.

## Error Codes

| Code | Meaning | Action |
|---|---|---|
| `401` | No API key | Provide API key |
| `429` | Rate limit exceeded | Slow down or upgrade |
| `10005` | Endpoint needs higher plan | Upgrade plan |
| `10010` | Pro key on Demo URL | Switch to `pro-api.coingecko.com` |
| `10011` | Demo key on Pro URL | Switch to `api.coingecko.com` |

## Common Mistakes

- **Guessing the plan tier.** Both keys start with `CG-`. Ask the user.
- **Mixing base URL and key type.** Pro key → `pro-api.coingecko.com`; Demo key → `api.coingecko.com`.
- **Using header AND query param** for the key at once. Pick one.
- **Guessing coin IDs.** Resolve via `/search` or `/coins/list`.
- **Wrong date format.** `/coins/{id}/history` wants `DD-MM-YYYY`, not ISO.
- **Trusting GeckoTerminal for well-known coins.** Prefer CoinGecko aggregated data; fall back to GeckoTerminal only for pools / DEX-native / unlisted tokens.

## Verify Before Responding

1. Correct base URL for the plan tier?
2. Correct auth header (`x-cg-pro-api-key` vs `x-cg-demo-api-key`)?
3. Coin IDs resolved (not guessed)?
4. CoinGecko preferred over GeckoTerminal for aggregated data?
5. Date/time params in the correct per-endpoint format?
