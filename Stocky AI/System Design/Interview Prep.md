---
tags:
  - stocky-ai
  - system-design
  - interview
created: 2026-04-07
status: complete
---

# Interview Prep

> [!tip] Key talking points for system design interviews and technical discussions about Stocky AI

## Quick Stats to Memorize

| Metric | Value |
|--------|-------|
| Frontend components | 50+ (27 card types) |
| Backend handlers | 31 |
| API endpoints | 40+ |
| LLM models | 4 |
| Groq API keys | 6 (round-robin, 180 RPM) |
| RSS news sources | 41 (8 categories) |
| Database tables | 14 (SQLite) |
| Agent architectures | 3 (Triad-3, Crew-7, Council-6) |
| Feature buttons | 20 |
| Commits | 79 in 60 days |
| Deploy frequency | 1.3/day (auto-deploy) |

## "If Asked About X, Say Y"

### "How does intent parsing work?"
2-layer system: (1) Regex NLP with 30+ patterns -- zero API cost, <1ms latency. (2) AI fallback via Groq Llama 3.3 70B with temperature 0.1 and JSON mode. Regex handles ~70% of queries, AI catches the rest.

### "How do you handle LLM rate limits?"
Round-robin key pool with 6 Groq API keys. Each key ~30 RPM free tier, so effective 180 RPM. `KeyPool` class with `asyncio.Lock()` for thread safety. On failure, next key is tried automatically (1 retry).

### "Why not use OpenAI/Claude?"
Groq is 10x faster inference (LPU hardware) and free tier. For deep research, I use Gemini 2.5 Pro via OpenRouter which has the best reasoning. Cost: $0 for 180 RPM vs $0.03/query on GPT-4.

### "How does the multi-agent debate work?"
3 architectures: Triad (3 agents: researcher -> skeptic -> synthesizer), Crew (7 sequential agents), Council (6 specialized agents across 3 rounds with CSO orchestrating). Council uses model routing: heavy agents (TS, FA, CSO) on 70B for depth, light agents (MP, RG, ME) on 17B for speed -- cuts latency by 40%.

### "How do you ensure trade safety?"
2-phase confirmation. Phase 1: intent capture creates `pending_action` in DB. Phase 2: frontend shows TradeConfirmation card, user must explicitly click "Confirm". No trade executes without Phase 2.

### "How does the 3-stage deep pipeline work?"
Stage 1: Primary analysis with button-specific prompt (1536-2048 tokens). Stage 2: Devil's Advocate critique at temp 0.3 (768 tokens) -- rates each claim as Verified/Plausible/Unverified/Refuted. Stage 3: Synthesis merges both into final verdict with Stocky Score 0-20.

### "What's your caching strategy?"
In-memory TTL cache with `@cached(ttl=N)` decorator. TTLs range from 10s (live quotes) to 3600s (fundamentals). MD5-hashed args as cache key. `clear_all_caches()` on Dhan token renewal.

### "How would you scale this to 50K users?"
Three phases: (1) Auth + PostgreSQL + Redis, (2) Kubernetes + Kafka + self-hosted vLLM, (3) Citus sharding + TimescaleDB + WebSocket gateway. LLM cost drops from $0.03/query (GPT-4) to $0.001/query (self-hosted 70B on A100).

### "What's the database design?"
14 SQLite tables via aiosqlite. Key tables: conversations (chat history with structured_data JSON), pending_actions (2-phase trades), trade_history, analytics_events, watchlist, alerts, feedback. At scale: shard by user_id, global market data on read replicas.

### "What would you change if starting over?"
PostgreSQL from day 1 (even for single user -- migration pain avoided). Redis for caching. Playwright tests (had 4 commits in 11 min reverting each other). Proper multi-tenant auth. But the ship-fast approach got to 79 commits in 60 days.

## Key Design Principles

1. **Mobile-first**: PWA with iOS/Android install, safe-area handling, 44px touch targets
2. **Data-backed**: Every AI claim cites sources; 0-20 scoring with factor breakdowns
3. **Contrarian edge**: AI personality challenges consensus, thinks in payoffs/asymmetry
4. **Ship daily**: Auto-deploy on push to main, 1.3 deploys/day
5. **Free-tier maximization**: Groq + Vercel + Railway = $0 infrastructure

## System Design Follow-Ups

**Q: How to add real-time price streaming?**
A: Dhan WebSocket -> Redis pub/sub -> WebSocket gateway (Centrifugo) -> client. Price updates pushed to all subscribed clients.

**Q: How to handle 100K LLM requests/min?**
A: Kafka topic `llm.requests` -> consumer group of vLLM workers (auto-scale on queue depth). Dead letter queue for failures. Groq as fallback for burst.

**Q: How to shard the database?**
A: Shard by `user_id` for conversations, trades, watchlist. Global tables (market data) on separate read-replica cluster. TimescaleDB for OHLCV tick data with 90-day compression.

## Related Notes
- [[Architecture]]
- [[Scaling Plan]]
- [[Tradeoffs]]
- [[Numbers]]
