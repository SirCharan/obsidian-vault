---
tags:
  - stocky-ai
  - system-design
  - architecture
created: 2026-04-07
status: complete
---

# Current Architecture

> [!info] As-is system design -- single-user, personal tool

## System Context

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
        DHAN["Dhan HQ v2"]
        KITE["Zerodha Kite"]
        YF["yfinance"]
        NSE["nsetools"]
        RSS["41 RSS Feeds"]
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

## Current Scale

| Metric | Current Value |
|--------|--------------|
| Requests per second | ~10 (single user) |
| Concurrent users | 1 |
| Data volume | ~50 MB (SQLite) |
| Database QPS | ~100 |
| Message rate | ~1 msg/s |
| Frontend components | 50+ |
| API endpoints | 40+ |
| Deploy frequency | 1.3/day |

## Key Design Choices

1. **Monolith backend**: Single FastAPI process handles everything -- chat, trading, market data, AI
2. **SQLite**: Zero-ops database, single-file backup, sufficient for single-user
3. **In-memory cache**: No Redis needed for single process
4. **Free-tier LLMs**: 6 Groq API keys in round-robin = 180 RPM for $0
5. **SSE for streaming**: Server-Sent Events for real-time agent debate updates

## Strengths of Current Design

- **Zero infrastructure cost** (Vercel free + Railway free + Groq free)
- **Sub-second intent parsing** via regex (no API call for common queries)
- **10x faster inference** than OpenAI via Groq LPU
- **Full PWA** with offline support, installable on mobile
- **1.3 deploys/day** velocity with auto-deploy on push

## Weaknesses

- Single-writer SQLite = cannot handle concurrent writes
- In-memory cache = lost on restart
- No test suite = regression risk
- localStorage JWT = not secure for multi-user
- yfinance 15-min delay = not real-time

## Related Notes
- [[Architecture]]
- [[Scaling Plan]]
- [[Tradeoffs]]
