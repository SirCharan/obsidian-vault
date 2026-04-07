---
tags:
  - stocky-ai
  - engineering
  - architecture
created: 2026-04-07
status: complete
---

# Architecture

> [!info] High-Level Design
> Client (PWA) -> Vercel Edge (CDN + CSP) -> FastAPI (Railway) -> LLM Providers (Groq/OpenRouter) + Market Data (Dhan/Kite/yfinance/RSS)

## System Architecture Diagram

```mermaid
graph TB
    subgraph Client["Client Layer"]
        PWA["PWA / Browser<br/>Next.js 16 + React 19"]
        SW["Service Worker<br/>Cache-first static<br/>Network-first API"]
    end

    subgraph Edge["Edge Layer -- Vercel"]
        CDN["Vercel CDN<br/>Static assets + ISR"]
        HEADERS["Security Headers<br/>CSP, X-Frame, HSTS"]
    end

    subgraph Backend["Backend -- Railway"]
        API["FastAPI + Uvicorn<br/>Async ASGI"]
        ORCH["LLM Orchestrator<br/>6-key round-robin"]
        CACHE["In-Memory TTL Cache<br/>10s -- 3600s"]
        DB["SQLite<br/>aiosqlite<br/>14 tables"]
    end

    subgraph LLMs["LLM Providers"]
        GROQ["Groq Cloud<br/>Llama 3.3 70B<br/>Scout 17B"]
        OR["OpenRouter<br/>Gemini 2.5 Pro"]
    end

    subgraph Data["Market Data"]
        DHAN["Dhan HQ v2<br/>Live quotes, Options<br/>OHLC, Historical"]
        KITE["Zerodha Kite<br/>Orders, Portfolio<br/>Holdings, Margins"]
        YF["yfinance<br/>Fundamentals<br/>Technicals"]
        NSE["nsetools<br/>Gainers, Losers<br/>Breadth"]
        RSS["41 RSS Feeds<br/>Indian + Global<br/>News sentiment"]
    end

    PWA --> CDN
    SW -.-> CDN
    CDN --> HEADERS --> API
    API --> ORCH --> GROQ
    ORCH --> OR
    API --> CACHE
    API --> DB
    API --> DHAN
    API --> KITE
    API --> YF
    API --> NSE
    API --> RSS
```

## Request Flow

1. User sends message via chat input
2. Frontend POST to `/api/chat` with `{message, conversation_id, deep}`
3. **Intent Parsing** (2-layer):
   - Layer 1: Regex NLP (`_parse_natural()`) -- 30+ regex patterns, zero API cost
   - Layer 2: AI Fallback (`interpret_intent()`) -- Groq Llama 3.3 70B, temp 0.1, JSON mode
4. Intent routes to one of **31 handlers** (analyse, scan, options, news, etc.)
5. Handler fetches market data (Dhan, yfinance, nsetools, RSS)
6. **LLM Orchestrator** enhances with AI analysis:
   - Quick mode: single Groq call (512-1024 tokens)
   - Deep mode: 3-stage pipeline (primary -> critique -> synthesis)
7. Response returns structured JSON + `ai_analysis` + `ai_metadata`
8. Frontend renders the appropriate **card component** via dynamic import

## Component Counts

| Layer | Count | Details |
|-------|-------|---------|
| Card components | 27 | Dynamic imports in MessageBubble.tsx |
| Backend handlers | 31 | analyse, scan, options, news, overview, etc. |
| API endpoints | 40+ | Chat, research, market data, trading, portfolio, export, analytics |
| Database tables | 14 | conversations, trades, watchlist, alerts, analytics, etc. |
| LLM models | 4 | Llama 3.3 70B, Scout 17B, GPT-OSS 120B, Gemini 2.5 Pro |
| RSS sources | 41 | 8 categories: Indian, Global, Commodities, Energy, Asia-Pacific, Geopolitical |

## Latency Profile

| Operation | Typical Latency |
|-----------|----------------|
| Regex intent parse | <1ms |
| AI intent parse (Groq) | 200-500ms |
| Quick analysis | 1-3s |
| Deep 3-stage pipeline | 5-12s |
| Triad research (3 agents) | 8-15s |
| Council research (6 agents) | 15-30s |
| Market data fetch (Dhan) | 100-300ms |
| yfinance fundamentals | 1-3s |
| RSS news aggregation | 2-5s |

## Related Notes
- [[Frontend Stack]]
- [[Backend Stack]]
- [[LLM Orchestration]]
- [[Current Architecture]]
