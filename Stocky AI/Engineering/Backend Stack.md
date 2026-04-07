---
tags:
  - stocky-ai
  - engineering
  - backend
created: 2026-04-07
status: complete
---

# Backend Stack

## Core Technologies

| Technology | Version | Role |
|-----------|---------|------|
| **FastAPI** | 0.115 | Async web framework (ASGI), auto-docs, Pydantic validation |
| **Uvicorn** | 0.34 | Production ASGI server |
| **Pydantic** | 2.9 | Request/response validation, JSON Schema |
| **aiosqlite** | 0.20 | Async SQLite (non-blocking DB access) |
| **httpx** | 0.28 | Async HTTP client (Dhan, OpenRouter) |
| **python-jose** | 3.3 | JWT token creation/validation |

## API Surface (40+ endpoints)

| Domain | Endpoints | Method |
|--------|-----------|--------|
| **Chat** | `/api/chat` | POST (intent parsing -> handler dispatch) |
| **Deep Research** | `/api/research`, `/api/deep-research`, `/api/crew-research`, `/api/council-research` | POST (SSE streaming) |
| **Market Data** | `/api/scan`, `/api/chart`, `/api/compare`, `/api/ipo`, `/api/macro`, `/api/rrg`, `/api/sectors`, `/api/valuation`, `/api/fii-dii`, `/api/options`, `/api/earnings`, `/api/dividends`, `/api/announcements` | GET/POST |
| **Trading** | `/api/trade/confirm`, `/api/kite/login`, `/api/kite/status` | POST/GET |
| **Portfolio** | `/api/conversations`, `/api/watchlist`, `/api/alerts` | CRUD |
| **Export** | `/api/export/pdf`, `/api/share` | POST |
| **Analytics** | `/api/analytics/log`, `/api/analytics/stats`, `/api/feedback` | POST/GET |

## 31 Handler Files

All in `backend/app/handlers/`:

| Handler | Purpose |
|---------|---------|
| `chat.py` | Intent parsing + dispatch to other handlers |
| `analyse.py` | Stock analysis (fundamentals + technicals + news) |
| `overview.py` | Market overview (indices, breadth, gainers/losers) |
| `news.py` | 41 RSS feed aggregation + sentiment scoring |
| `scan.py` | 7 scan types (volume pump, breakout, etc.) |
| `options.py` | Options chain analytics (PCR, Max Pain, IV, Greeks) |
| `chart.py` | TradingView chart embedding + technical data |
| `compare.py` | Head-to-head stock comparison |
| `deep_research.py` | OpenRouter Gemini 2.5 Pro deep research |
| `agent_debate.py` | Triad 3-agent debate (SSE streaming) |
| `crew_research.py` | Crew 7-agent pipeline (SSE streaming) |
| `council.py` | Council 6-agent debate (SSE streaming) |
| `trading.py` | Trade execution via Kite Connect |
| `portfolio.py` | Holdings, positions, margins from Kite |
| `ipo.py` | IPO data aggregation |
| `macro.py` | Macro indicators (crude, gold, USDINR, VIX) |
| `rrg.py` | Relative Rotation Graphs (sector vs Nifty) |
| `sectors.py` | Sector performance analysis |
| `valuation.py` | Market PE/PB valuation metrics |
| `fii_dii.py` | FII/DII flow data |
| `earnings.py` | Upcoming earnings calendar |
| `dividends.py` | Dividend data and history |
| `announcements.py` | Corporate announcements |
| `top_stocks.py` | Multi-scan top stocks dashboard |
| `market.py` | Market price lookup |
| `alerts.py` | Price alert CRUD |
| `watchlist.py` | Watchlist CRUD |
| `export_pdf.py` | PDF export of cards |
| `share.py` | Shareable card snapshots |

## Intent Parsing (2-layer)

1. **Regex NLP** (`_parse_natural()`): 30+ regex patterns, zero API cost
   - `"how's the market"` -> `overview`
   - `"analyse RELIANCE"` -> `analyse, [RELIANCE]`
   - `"buy 10 INFY at 1500"` -> `buy, [INFY, 10, 1500]`
2. **AI Fallback** (`interpret_intent()`): Groq Llama 3.3 70B, temp 0.1, JSON mode

## Caching Architecture

In-memory TTL cache with `@cached(ttl=N)` decorator, MD5-hashed args for cache key:

| Data Type | TTL | Rationale |
|-----------|-----|-----------|
| Live quotes (Dhan) | 10-30s | Near real-time requirement |
| Scan results | 120s | Expensive batch download (yfinance 100 stocks) |
| Technical indicators | 300s | Computed from daily data, stable intraday |
| Options analytics | 300s | Chain data changes moderately |
| Fundamentals | 3600s | Quarterly data, rarely changes |
| News feeds | 1800s | RSS feeds update every 15-30 min |

## Pydantic Models

Key request/response models in `models.py`:

| Model | Fields |
|-------|--------|
| `ChatRequest` | message, conversation_id, deep |
| `ChatResponse` | type, content, data, action_id, conversation_id |
| `TradeActionRequest` | action_id, action (confirm/cancel) |
| `ResearchRequest` | stock, mode |
| `ScanRequest` | scan_type |
| `AlertRequest` | symbol, direction, target_price |
| `AgentDebateRequest` | query, conversation_id |

## Related Notes
- [[Architecture]]
- [[Database Schema]]
- [[LLM Orchestration]]
- [[Data Pipeline]]
