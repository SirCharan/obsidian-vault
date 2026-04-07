---
tags:
  - stocky-ai
  - overview
created: 2026-04-07
status: complete
---

# Stocky AI Knowledge Base

> [!info] Quick Reference
> **URL**: [llm.stockyai.xyz](https://llm.stockyai.xyz)
> **Repo**: `SirCharan/twitter` (monorepo, `osaka/stocky-web/`)
> **Built by**: Charandeep Kapoor (CK) -- IIT Kanpur, NISM certified
> **Stack**: Next.js 16 + React 19 | FastAPI | Groq + OpenRouter | Zerodha + Dhan

## What is Stocky AI?

A personal AI-powered trading assistant for Indian equity markets (NSE/BSE). It combines real-time market data, multi-agent LLM reasoning, and broker integration into a single chat-based interface -- designed to feel like **Bloomberg Terminal meets ChatGPT**.

## By the Numbers

| Metric | Value |
|--------|-------|
| Frontend components | 50+ (27 card types) |
| Backend handlers | 31 |
| LLM models used | 4 (Llama 3.3 70B, Scout 17B, GPT-OSS 120B, Gemini 2.5 Pro) |
| Groq API keys | 6 (round-robin pool) |
| RSS news sources | 41 |
| Database tables | 14 |
| Agent architectures | 3 (Triad 3-agent, Crew 7-agent, Council 6-agent) |
| Feature buttons | 20 |
| Commits | 79 in 60 days (1.3 deploys/day) |

## Navigation

### Engineering
- [[Architecture]] -- Full system architecture with Mermaid diagrams
- [[Frontend Stack]] -- Next.js 16, React 19, Tailwind, PWA
- [[Backend Stack]] -- FastAPI, handlers, database, caching
- [[LLM Orchestration]] -- Models, key pool, prompts, 3-stage pipeline
- [[Multi-Agent Debate]] -- Triad, Crew, Council architectures
- [[Data Pipeline]] -- Market data sources, RSS feeds, options analytics
- [[Trading Integration]] -- Kite Connect, Dhan HQ, 2-phase trade flow
- [[Security]] -- CSP, auth, CORS, trade safety
- [[Deployment]] -- Vercel + Railway, CI/CD, SW versioning
- [[Tradeoffs]] -- Every engineering decision + why + limitation

### System Design
- [[Current Architecture]] -- As-is design with Mermaid diagrams
- [[Scaling Plan]] -- 10K RPS / 50K concurrent target design
- [[Database Schema]] -- All 14 tables, indexes, relationships
- [[Interview Prep]] -- Key talking points, numbers, design principles

### Product
- [[Features]] -- All 20 feature buttons
- [[Cards]] -- All 27 card components
- [[AI Agents]] -- Agent personalities, prompts, debate flows
- [[Roadmap]] -- Near-term, medium-term, long-term

### Social
- [[Pitch]] -- 1-liner, elevator, detailed pitch
- [[Demo Script]] -- Step-by-step demo flow
- [[Technical Story]] -- How I built a Bloomberg-like AI trading terminal
- [[Numbers]] -- Key metrics for conversations

## Related Notes
- [[Architecture]]
- [[Interview Prep]]
- [[Pitch]]
