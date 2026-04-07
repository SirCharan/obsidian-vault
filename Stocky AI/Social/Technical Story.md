---
tags:
  - stocky-ai
  - social
  - story
created: 2026-04-07
status: complete
---

# Technical Story

## How I Built a Bloomberg-Like AI Trading Terminal

### The Problem

As a trader with 6+ years in crypto and stocks, I was using 5+ tools every day: Zerodha for trading, Screener for fundamentals, TradingView for charts, Moneycontrol for news, and Twitter for sentiment. I wanted one interface that could do it all -- and think for me.

### The Build

**60 days. 79 commits. 1.3 deploys per day.**

Started with a simple chat interface and a single Groq API key. The first version could answer basic stock questions. Then I kept adding:

**Week 1-2**: Built the intent parsing system. 30+ regex patterns handle common queries at zero API cost and <1ms latency. AI fallback catches everything else.

**Week 3-4**: Added 20 feature buttons, each with its own backend handler. Market overview, stock analysis, scanning, comparison, options analytics. Every handler follows the same pattern: fetch data -> cache -> LLM orchestrate -> return structured JSON.

**Week 5-6**: Built the multi-agent debate system. Started with Triad (3 agents: researcher, skeptic, synthesizer). Then added Crew (7 sequential agents). Finally, the Council -- 6 specialized agents debating across 3 rounds with SSE streaming. The model routing trick: heavy agents (TS, FA, CSO) use 70B for depth, light agents (MP, RG, ME) use 17B for speed. Cuts latency by 40%.

**Week 7-8**: LLM orchestration upgrade. Created 16 button-specific prompt configs with 0-20 scoring systems. Added the 3-stage deep pipeline (analysis -> Devil's Advocate critique -> synthesis). Built the round-robin key pool across 6 Groq API keys for 180 RPM at $0.

### The Architecture

Frontend: Next.js 16 + React 19 PWA with 27 dynamically-imported card components. Each card handles a specific data shape -- from stock analysis to options chains to council debate results.

Backend: FastAPI with 31 handlers, async everywhere. SQLite via aiosqlite for zero-ops persistence. In-memory TTL cache (10s-3600s). Two broker integrations (Zerodha Kite + Dhan HQ) with auto-renewing tokens.

LLM: 4 models (Llama 3.3 70B, Scout 17B, GPT-OSS 120B, Gemini 2.5 Pro). 6 API keys in round-robin. 3 multi-agent architectures with SSE streaming.

Data: 5 market data sources (Dhan, Kite, yfinance, nsetools, 41 RSS feeds). Full options analytics pipeline (PCR, Max Pain, IV skew, OI interpretation).

### The Key Insight

The biggest insight was **model routing in multi-agent debate**. Not every agent needs the biggest model. The Risk Guardian just needs to flag risks -- 17B is fine. But the Fundamental Analyst needs to deeply analyze financial ratios -- give it the 70B. This simple routing cut latency by 40% while maintaining quality where it matters.

### What I'd Do Differently

PostgreSQL from day 1 (even for single user). Playwright E2E tests from the start (had 4 commits in 11 minutes reverting each other). But the ship-fast approach worked -- 79 commits in 60 days got me to a fully functional AI trading terminal.

## Related Notes
- [[Pitch]]
- [[Architecture]]
- [[Numbers]]
