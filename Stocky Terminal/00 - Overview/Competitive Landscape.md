---
title: Competitive Landscape
date: 2026-04-07
tags:
  - stocky-terminal
  - competition
  - market-analysis
  - open-source
status: published
category: overview
---

# Competitive Landscape

Over 20 open-source financial projects were researched to understand the competitive landscape and identify Stocky Terminal's unique positioning.

> [!info] Research Scope
> Projects evaluated span financial data platforms, AI trading agents, portfolio trackers, and OSINT tools. Stars counts as of early 2026.

## Major Competitors

| Project | Stars | Category | Stack | Focus |
|---|---|---|---|---|
| **OpenBB** | 65K+ | Data Platform | Python | Institutional-grade financial data SDK |
| **World Monitor** | 47K+ | OSINT | Tauri + Rust | 45+ OSINT layers, desktop app |
| **TradingAgents** | 48K+ | AI Trading | Python | Multi-agent AI debate for signals |
| **FinGPT** | 19K+ | Financial LLM | Python | Fine-tuned financial language model |
| **Ghostfolio** | 8K+ | Portfolio | Angular + NestJS | Portfolio tracking + analysis |
| **Screeni-py** | 677+ | Screener | Python | NSE stock screening CLI |

## Detailed Analysis

### OpenBB (65K stars)
- **What it does:** Python-based financial data platform with SDK, Terminal Pro, and API
- **Strengths:** Massive community, institutional adoption, comprehensive data coverage
- **Gap:** Python-only, no browser UI for casual users, no OSINT, no India-specific features
- **Stocky advantage:** Browser-based, India-focused, combines OSINT + market data

### World Monitor (47K stars)
- **What it does:** Tauri desktop app with 45+ OSINT data layers on a global map
- **Strengths:** Excellent OSINT coverage, fast desktop app, beautiful visualization
- **Gap:** Desktop-only (no web), no market data integration, no AI signals, no India focus
- **Stocky advantage:** Web PWA, live market data, AI signals, India-specific data

### TradingAgents (48K stars)
- **What it does:** Multi-agent AI system where bull/bear/neutral agents debate trade decisions
- **Strengths:** Innovative architecture, sophisticated signal generation
- **Gap:** Research project, no live UI, no market data pipeline, no India focus
- **Stocky advantage:** Production-ready, live data, full UI, deployed and serving users

### FinGPT (19K stars)
- **What it does:** Open-source financial LLM with fine-tuning frameworks
- **Strengths:** Purpose-built for financial NLP, sentiment analysis
- **Gap:** Model toolkit, not a product; no UI, no live data pipeline
- **Stocky advantage:** Complete product with UI, data, AI, and distribution

### Ghostfolio (8K stars)
- **What it does:** Privacy-first portfolio tracking with performance analytics
- **Strengths:** Clean UI, self-hostable, multi-currency support
- **Gap:** Portfolio tracking only, no live trading data, no AI, no OSINT
- **Stocky advantage:** Real-time terminal, not just portfolio tracking

### Screeni-py (677 stars)
- **What it does:** NSE stock screener with technical + fundamental filters
- **Strengths:** India-focused, good screening logic
- **Gap:** CLI-only, no web UI, no AI, no OSINT, limited to screening
- **Stocky advantage:** Full terminal experience, not just screening

## Stocky Terminal's Moat

> [!tip] Unique Positioning
> Stocky Terminal is the **only** project that combines all four pillars in a single browser-based product:
> 1. **India market data** (NSE/BSE live quotes, FII/DII, options chain)
> 2. **Geopolitical OSINT** (27+ map layers, conflict tracking, disaster monitoring)
> 3. **AI trade signals** (Groq-powered generation, validation, aggregation)
> 4. **Automated daily briefs** (8AM/8PM IST, email distribution, blog)

## Competitive Matrix

| Feature | Stocky | OpenBB | World Monitor | TradingAgents | Ghostfolio |
|---|---|---|---|---|---|
| Browser-based | Yes | No | No | No | Yes |
| India market data | Yes | Partial | No | No | Partial |
| OSINT map | Yes (27+ layers) | No | Yes (45+ layers) | No | No |
| AI signals | Yes | No | No | Yes | No |
| Daily briefs | Yes | No | No | No | No |
| Options chain | Yes | Yes | No | No | No |
| PWA / Offline | Yes | N/A | N/A | N/A | Yes |
| Push notifications | Yes | No | No | No | No |
| Zero frameworks | Yes | N/A | N/A | N/A | No (Angular) |
| Open source | Yes (AGPL-3.0) | Yes | Yes | Yes | Yes (AGPL-3.0) |

## Market Opportunity

The Indian retail trading market has grown explosively:
- **150M+ demat accounts** (as of 2025, up from 40M in 2020)
- **NSE daily turnover** exceeds $100B in derivatives
- **Bloomberg Terminal** costs $24,000/year — inaccessible to retail traders
- **No free alternative** covers India-specific data comprehensively

> [!warning] Defensibility
> The primary risk is that larger platforms (OpenBB, TradingView) add India-specific features. Stocky's defense is speed of iteration, OSINT integration (unique in finance), and community-driven development under AGPL-3.0.

## Related Notes

- [[Project Overview]]
- [[Tech Stack]]
- [[Future Roadmap]]
- [[Architecture Decisions]]
