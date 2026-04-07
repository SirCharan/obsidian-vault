---
tags:
  - stocky-ai
  - engineering
  - tradeoffs
created: 2026-04-07
status: complete
---

# Tradeoffs

> [!info] Every engineering decision with rationale and limitation

## Architecture Decisions

| Decision | What We Chose | Alternative | Why | Limitation |
|----------|--------------|-------------|-----|------------|
| Database | SQLite | PostgreSQL | Zero ops, instant backup, sufficient for single-user | Single-writer, no replication, no concurrent writes |
| LLM Provider | Groq (free tier, 6 keys) | OpenAI GPT-4, Anthropic Claude | 10x faster inference (LPU hardware), $0 cost | Smaller models, rate limits |
| Frontend Framework | Next.js 16 + React 19 | SvelteKit, Remix | Best ecosystem, SSR + SSG + ISR, Vercel integration | Large bundle, complex hydration |
| Styling | Tailwind v4 (PostCSS) | CSS Modules, Styled Components | Utility-first = fast iteration, small CSS | Bleeding-edge; no tailwind.config.ts customization yet |
| Animations | Framer Motion (190KB) | CSS transitions, React Spring | Best DX, spring physics, layoutId | 190KB bundle (mitigated by dynamic imports) |
| Market Data | yfinance + Dhan + nsetools | Bloomberg API, Refinitiv | Free, sufficient data quality | yfinance 15-min delay, nsetools unreliable |
| Caching | In-memory dict + TTL | Redis, Memcached | Zero infra | Lost on restart, no cross-process sharing |
| Auth | Hardcoded "CK" | Auth0, Clerk, NextAuth | Personal tool, no multi-user needed | Zero security for multi-tenant |
| Testing | None | Jest + Playwright | Max velocity | Regressions (4 commits in 11 min reverting each other) |
| News | 41 RSS feeds + keyword sentiment | NLP models, paid APIs | Free, comprehensive coverage | No semantic understanding, keyword false positives |
| Intent Parsing | Regex + AI fallback | Full NLP/vector search | Fast, deterministic, zero API cost for regex hits | Brittle, no fuzzy matching |
| Backend Framework | FastAPI | Django | Async-native, faster, lighter | No admin panel, no ORM, manual migrations |
| Validation | Pydantic v2 | Marshmallow, attrs | 5-40x faster validation | Breaking changes from v1 |

## Frontend Tradeoffs

| Decision | Tradeoff |
|----------|----------|
| Tailwind v4 (PostCSS) | Bleeding-edge; no tailwind.config.ts customization yet |
| Framer Motion (190KB) | Rich animations vs bundle size; offset by dynamic imports |
| localStorage for auth | XSS risk vs simplicity (single-user personal tool) |
| No test suite | Ship velocity vs regression safety |
| "use client" on all components | Correct for interactive cards, but limits Server Component benefits |
| html2canvas for share | Can hang on complex cards; mitigated with 8s timeout |

## Backend Tradeoffs

| Decision | Tradeoff |
|----------|----------|
| SQLite (not PostgreSQL) | Zero ops, instant setup. But: single-writer, no replication |
| In-memory cache (not Redis) | Zero infra. But: lost on restart |
| Regex intent parsing | Fast, zero API cost. But: brittle, no fuzzy matching |

## LLM Tradeoffs

| Decision | Tradeoff |
|----------|----------|
| Groq (not OpenAI) | 10x faster, free. But: smaller models, less reliable |
| 6-key round-robin | 180 RPM free. But: fragile if Groq changes limits |
| Prompt-per-button | Tailored output. But: 16 prompts to maintain, drift risk |
| 3-stage deep pipeline | Higher quality. But: 3x latency, 3x cost |
| Gemini via OpenRouter | Best reasoning for deep research. But: additional API dependency |

## What Would Break at Scale

| Current State | Breaks At | Fix Required |
|--------------|-----------|-------------|
| SQLite | >10 concurrent writers | PostgreSQL + connection pooling |
| In-memory cache | >1 server instance | Redis cluster |
| 6 Groq keys | >180 RPM | Enterprise Groq or self-hosted vLLM |
| Single FastAPI process | >500 concurrent | K8s horizontal pod autoscaler |
| localStorage JWT | >1 user | HttpOnly cookies + refresh tokens |
| yfinance | Real-time requirement | WebSocket market data feed |
| RSS feed parsing | >1000 req/min | Async job queue (Celery/NATS) |

## Related Notes
- [[Architecture]]
- [[Scaling Plan]]
- [[Interview Prep]]
