---
tags:
  - stocky-ai
  - product
  - features
created: 2026-04-07
status: complete
---

# Features

## 20 Feature Buttons

| # | Button | Handler | What It Does |
|---|--------|---------|-------------|
| 1 | **Market Overview** | `overview.py` | Indices, breadth, gainers/losers, VIX, FII/DII snapshot |
| 2 | **Top Stocks** | `top_stocks.py` | Multi-scan dashboard (gainers, volume, breakouts, losers, sectors) |
| 3 | **Analyse** | `analyse.py` | Deep stock analysis (fundamentals + technicals + news + AI verdict) |
| 4 | **Deep Research** | `deep_research.py` | Gemini 2.5 Pro deep research via OpenRouter |
| 5 | **Scan** | `scan.py` | 7 scan types (volume pump, breakout, momentum, etc.) |
| 6 | **Chart** | `chart.py` | TradingView chart embed + technical indicator overlay |
| 7 | **Compare** | `compare.py` | Head-to-head stock comparison (8+ metrics) |
| 8 | **Options** | `options.py` | Option chain analytics (PCR, Max Pain, IV, OI, strategies) |
| 9 | **IPO** | `ipo.py` | Upcoming/current IPOs with verdicts |
| 10 | **Macro** | `macro.py` | Macro dashboard (crude, gold, USDINR, VIX, yields) |
| 11 | **RRG** | `rrg.py` | Relative Rotation Graphs (sector rotation vs Nifty) |
| 12 | **Sectors** | `sectors.py` | Sector performance analysis and rotation signals |
| 13 | **Valuation** | `valuation.py` | Market PE/PB valuation metrics and regime |
| 14 | **FII/DII** | `fii_dii.py` | Institutional flow data and analysis |
| 15 | **Earnings** | `earnings.py` | Upcoming earnings calendar with AI analysis |
| 16 | **Dividends** | `dividends.py` | Dividend data, history, and yield analysis |
| 17 | **Announcements** | `announcements.py` | Corporate announcements and filings |
| 18 | **Summarise** | Chat handler | AI-powered text summarization |
| 19 | **Portfolio** | `portfolio.py` | Holdings, positions, margins from Kite Connect |
| 20 | **News** | `news.py` | 41 RSS feed aggregation with sentiment scoring |

## Deep Research Modes

| Mode | Agents | Model | Streaming |
|------|--------|-------|-----------|
| **Quick** | 1 (orchestrator) | Llama 3.3 70B | No |
| **Deep** (3-stage) | 1 + critique | Llama 3.3 70B | No |
| **Triad** | 3 (Aris/Silas/Nexus) | Scout 17B | SSE |
| **Crew** | 7 (sequential pipeline) | Scout 17B | SSE |
| **Council** | 6 (3 rounds) | 70B heavy + 17B light | SSE |

## 7 Scan Types

Available via the Scan button:
- Volume Pump
- Breakout
- Momentum
- Oversold Bounce
- 52-Week High/Low
- Sector Rotation
- Delivery Pickup

## Related Notes
- [[Cards]]
- [[AI Agents]]
- [[LLM Orchestration]]
