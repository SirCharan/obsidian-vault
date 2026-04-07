---
title: System Architecture
date: 2026-04-07
tags:
  - stocky-terminal
  - architecture
  - system-design
  - vercel
  - edge-functions
status: published
category: architecture
---

# System Architecture

Stocky Terminal follows a JAMstack-inspired architecture: a static frontend deployed as a PWA communicates with 30+ Vercel Edge Functions that aggregate data from multiple upstream sources, cached via Upstash Redis.

> [!info] Design Principles
> 1. **Edge-first** — All API logic runs at the edge (Vercel Edge Functions), not in a traditional server
> 2. **Cache-heavy** — Redis caching at every layer reduces upstream API calls and latency
> 3. **Graceful degradation** — Race patterns and fallback chains ensure data availability
> 4. **Zero backend state** — No database beyond Redis cache; the client is the source of truth for user preferences

## Full System Architecture

```mermaid
flowchart TB
    subgraph Browser["Browser (PWA)"]
        direction TB
        UI["Vanilla TS UI<br/>12+ Panels"]
        SW["Service Worker<br/>App Shell Cache"]
        IDB["IndexedDB<br/>Event Store"]
        LS["localStorage<br/>Preferences"]
        UI <--> SW
        UI <--> IDB
        UI <--> LS
    end

    subgraph Vercel["Vercel Edge Functions"]
        direction TB
        MARKET["Market APIs<br/>/api/market/*"]
        DATA["Data APIs<br/>/api/data/*"]
        AI["AI APIs<br/>/api/ai/*"]
        EMAIL["Email APIs<br/>/api/email/*"]
        CRON["Cron Jobs<br/>5 scheduled"]
    end

    subgraph Upstream["Data Sources"]
        direction TB
        ZER["Zerodha Kite Connect"]
        DHAN["Dhan API"]
        YAHOO["Yahoo Finance"]
        NSE["NSE India"]
        FINN["Finnhub"]
        COIN["CoinGecko"]
        RSS["333+ RSS Feeds"]
        ACLED_S["ACLED"]
        USGS_S["USGS"]
        NASA_S["NASA EONET/FIRMS"]
        GDACS_S["GDACS"]
        CF["Cloudflare Radar"]
    end

    subgraph Services["External Services"]
        REDIS["Upstash Redis"]
        GROQ["Groq API<br/>Llama 3.3 70B"]
        RESEND["Resend<br/>Email Delivery"]
        PUSH["Web Push<br/>VAPID"]
        OLLAMA["Ollama<br/>Local Fallback"]
    end

    Browser --> Vercel
    MARKET --> ZER & DHAN & YAHOO & NSE & FINN & COIN
    DATA --> RSS & ACLED_S & USGS_S & NASA_S & GDACS_S & CF
    AI --> GROQ
    AI -.-> OLLAMA
    EMAIL --> RESEND
    CRON --> REDIS
    CRON --> GROQ
    CRON --> RESEND
    MARKET --> REDIS
    DATA --> REDIS
    AI --> REDIS
    CRON --> PUSH
```

## Request Flow

A typical market data request follows this path:

```mermaid
sequenceDiagram
    participant B as Browser
    participant V as Vercel Edge
    participant R as Upstash Redis
    participant Z as Zerodha
    participant D as Dhan
    participant Y as Yahoo Finance

    B->>V: GET /api/market/quote?symbol=RELIANCE
    V->>R: Check cache
    alt Cache hit
        R-->>V: Cached quote
        V-->>B: 200 (s-maxage hit)
    else Cache miss
        V->>Z: Fetch quote
        V->>D: Fetch quote (parallel)
        V->>Y: Fetch quote (parallel)
        Note over V: Race pattern: first valid response wins
        Z-->>V: Quote data
        V->>R: Cache result
        V-->>B: 200 + Cache-Control headers
    end
```

## Edge Function Regions

| Region | Code | Purpose |
|---|---|---|
| US East (Virginia) | IAD | Default, closest to Upstash Redis |
| Singapore | SIN | Asia-Pacific users |
| Mumbai | BOM | India users, lowest latency to NSE |

## Data Flow Rates

| Pipeline | Interval | Source | Cache TTL |
|---|---|---|---|
| Ticker quotes | 15s | Zerodha/Dhan/Yahoo | 10s edge, 15s Redis |
| Market overview | 15s | Yahoo Finance | 15s |
| Commodities | 30s | Yahoo Finance | 30s |
| RSS feeds | 15min | 333+ feeds | 15min |
| Weather | 30min | OpenWeatherMap | 30min |
| AI signals | 5min | Groq API | 5min |
| X feed | 2min | X API | 2min |
| YouTube | 5min | YouTube API | 5min |

## Cron Job Schedule

| Job | Schedule | Description |
|---|---|---|
| Morning Brief | 8:00 AM IST (Mon-Fri) | Generate + email daily morning brief |
| Evening Brief | 8:00 PM IST (Mon-Fri) | Generate + email daily evening brief |
| Insight Generation | Every 15 minutes | Pre-cache AI insights from high-severity headlines |
| Signal Validation | Every 2 hours | Validate existing signals against live prices |
| Signal Aggregation | Every hour | Aggregate and score trade signals |

> [!warning] Single Point of Failure
> Upstash Redis is the most critical dependency. If Redis is down, the blog, AI insights, signals, email ratings, and edition numbering all fail. The market data APIs can still function (they fall back to upstream sources directly), but caching is lost.

## Security Model

- All Edge Functions validate input parameters
- CORS headers configured for terminal.stockyai.xyz origin
- No user authentication (public terminal) — future consideration
- API keys stored as Vercel environment variables, never in client code
- Zerodha access token refreshed daily via GitHub Actions (never stored in Redis)

## Related Notes

- [[Frontend Architecture]]
- [[API Layer Design]]
- [[Data Pipeline Architecture]]
- [[Database & Caching]]
- [[Deployment]]
- [[Tech Stack]]
