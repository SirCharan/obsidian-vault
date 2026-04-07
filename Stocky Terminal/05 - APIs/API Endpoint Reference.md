---
title: API Endpoint Reference
date: 2026-04-07
tags:
  - stocky-terminal
  - api
  - endpoints
  - reference
  - vercel-edge
status: published
category: apis
---

# API Endpoint Reference

Complete reference for Stocky Terminal's 30+ Vercel Edge Function endpoints.

> [!info] Base URL
> Production: `https://terminal.stockyai.xyz/api`
> All endpoints return JSON with `Content-Type: application/json` and CORS headers.

## Market Data Endpoints

| Method | Path | Description | Cache |
|---|---|---|---|
| GET | `/api/market/quote` | Single stock quote (race pattern: Zerodha → Dhan → Yahoo) | `s-maxage=10, swr=20` |
| GET | `/api/market/batch` | Batch quotes for multiple symbols | `s-maxage=15, swr=30` |
| GET | `/api/market/chart` | OHLC chart data for a symbol | `s-maxage=15, swr=60` |
| GET | `/api/market/overview` | Market overview (indices, sectors) | `s-maxage=15, swr=30` |
| GET | `/api/market/options` | Options chain with Greeks | `s-maxage=10, swr=20` |
| GET | `/api/market/commodities` | Gold, Silver, Crude, NatGas, Copper | `s-maxage=30, swr=60` |
| GET | `/api/market/crypto` | 25 cryptocurrency prices | `s-maxage=30, swr=60` |
| GET | `/api/market/forex` | Major forex pairs inc. USD/INR | `s-maxage=60, swr=120` |
| GET | `/api/market/gift-nifty` | Gift Nifty (SGX) pre-market | `s-maxage=30, swr=60` |
| GET | `/api/market/52w-scanner` | 52-week high/low scanner | `s-maxage=60, swr=120` |
| GET | `/api/market/ticker` | Ticker bar data (top symbols) | `s-maxage=10, swr=20` |

## Data & Intelligence Endpoints

| Method | Path | Description | Cache |
|---|---|---|---|
| GET | `/api/data/news` | Aggregated RSS news feed | `s-maxage=900, swr=1800` |
| GET | `/api/data/fii-dii` | FII/DII institutional flow data | `s-maxage=300, swr=600` |
| GET | `/api/data/country-profile` | Country dossier (30 countries) | `s-maxage=3600, swr=7200` |
| GET | `/api/data/india-macro` | India macro dashboard | `s-maxage=3600, swr=7200` |
| GET | `/api/data/corporate-actions` | Dividends, splits, bonuses | `s-maxage=3600, swr=7200` |
| GET | `/api/data/bulk-deals` | NSE bulk/block deals | `s-maxage=300, swr=600` |
| GET | `/api/data/osint/conflicts` | ACLED armed conflict data | `s-maxage=3600, swr=7200` |
| GET | `/api/data/osint/earthquakes` | USGS earthquakes M5+ | `s-maxage=300, swr=600` |
| GET | `/api/data/osint/fires` | NASA FIRMS active fires | `s-maxage=3600, swr=7200` |
| GET | `/api/data/osint/disasters` | GDACS disaster alerts | `s-maxage=1800, swr=3600` |
| GET | `/api/data/osint/outages` | Cloudflare Radar internet outages | `s-maxage=3600, swr=7200` |
| GET | `/api/data/osint/flights` | OpenSky flight positions | `s-maxage=10, swr=30` |
| GET | `/api/data/osint/vessels` | AIS vessel positions | `s-maxage=60, swr=120` |
| GET | `/api/data/weather` | Weather for Indian cities | `s-maxage=1800, swr=3600` |

## AI Endpoints

| Method | Path | Description | Cache |
|---|---|---|---|
| GET | `/api/ai/insight` | Pre-cached AI insight for an asset | `s-maxage=300, swr=600` |
| POST | `/api/ai/analyze` | On-demand symbol analysis | No cache |
| POST | `/api/ai/search` | AI-powered search summary | No cache |
| GET | `/api/ai/signals` | Active trade signals | `s-maxage=60, swr=120` |
| POST | `/api/ai/fed-impact` | FED policy impact analysis | No cache |

## Blog & Email Endpoints

| Method | Path | Description | Cache |
|---|---|---|---|
| GET | `/api/blog/posts` | List all briefs (paginated) | `s-maxage=60, swr=120` |
| GET | `/api/blog/post` | Single brief by edition | `s-maxage=3600, swr=7200` |
| GET | `/api/blog/latest` | Latest brief | `s-maxage=60, swr=120` |
| POST | `/api/email/subscribe` | Subscribe to daily briefs | No cache |
| POST | `/api/email/unsubscribe` | Unsubscribe | No cache |
| POST | `/api/email/rate` | Rate a brief (1-10) | No cache |

## Push & Cron Endpoints

| Method | Path | Description | Auth |
|---|---|---|---|
| POST | `/api/push/subscribe` | Register push subscription | No auth |
| POST | `/api/push/send` | Send push notification | Cron secret |
| POST | `/api/cron/brief` | Generate daily brief | Cron secret |
| POST | `/api/cron/insights` | Generate AI insights | Cron secret |
| POST | `/api/cron/validate` | Validate active signals | Cron secret |
| POST | `/api/cron/aggregate` | Aggregate signals | Cron secret |

## Common Query Parameters

| Parameter | Type | Used By | Description |
|---|---|---|---|
| `symbol` | string | quote, chart, analyze | Stock symbol (e.g., "RELIANCE", "NIFTY 50") |
| `range` | string | chart | "1D", "1W", "1M", "3M", "1Y" |
| `interval` | string | chart | "1m", "5m", "1d" |
| `index` | string | options | "NIFTY", "BANKNIFTY", "SENSEX", "FINNIFTY", "MIDCPNIFTY" |
| `country` | string | country-profile | ISO 3166-1 alpha-2 code |
| `edition` | number | blog/post | Brief edition number |
| `page` | number | blog/posts | Pagination (default: 1) |
| `limit` | number | blog/posts | Items per page (default: 10) |

> [!warning] Authentication
> Cron endpoints require a `CRON_SECRET` header matching the Vercel environment variable. All other endpoints are public (no auth required). Future authenticated features will use JWT tokens.

> [!tip] Cache Notation
> `s-maxage=10, swr=20` means: Vercel CDN serves cached response for 10s, then serves stale for another 20s while revalidating in the background. Total: user sees cached data for up to 30s, but gets fresh data within 10s on average.

## Related Notes

- [[API Layer Design]]
- [[India-Specific APIs]]
- [[System Architecture]]
- [[Database & Caching]]
