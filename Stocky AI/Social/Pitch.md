---
tags:
  - stocky-ai
  - social
  - pitch
created: 2026-04-07
status: complete
---

# Pitch

## One-Liner
**Stocky AI is Bloomberg Terminal meets ChatGPT for Indian retail investors -- AI-powered market analysis, multi-agent debate, and broker-integrated trading in a single chat interface.**

## 30-Second Elevator Pitch

I built an AI trading assistant that combines real-time market data from 5 sources, 41 RSS news feeds, and multi-agent LLM reasoning into a chat-based interface. You can analyse any stock with a Stocky Score 0-20, get 6 AI agents debating your trade thesis in real-time via SSE, and execute trades through Zerodha/Dhan -- all from one chat. It runs 4 LLM models across 6 API keys in round-robin for 180 RPM at zero cost. Built in 60 days, 79 commits, shipping 1.3 times a day.

## 2-Minute Detailed Pitch

**Problem**: Indian retail investors use 5+ tools: broker apps for trading, Screener for fundamentals, TradingView for charts, Moneycontrol for news, Twitter for sentiment. No single tool gives you AI-powered analysis + real-time data + trade execution.

**Solution**: Stocky AI -- a personal AI trading terminal. Type "analyse RELIANCE" and get a Stocky Score 0-20 with fundamental, technical, sentiment, and macro breakdowns. Ask for deep research and 6 specialized AI agents (Technical Strategist, Fundamental Analyst, Risk Guardian, Macro Economist, Market Pulse, Chief Synthesis Officer) debate your thesis across 3 rounds with a final confidence score.

**Technical edge**:
- 4 LLM models (Llama 3.3 70B, Scout 17B, GPT-OSS 120B, Gemini 2.5 Pro) via Groq + OpenRouter
- 6 API keys in round-robin = 180 RPM at $0
- 3-stage deep pipeline: analysis -> Devil's Advocate critique -> synthesis
- 41 RSS feeds with keyword sentiment scoring
- Full PWA with offline support, installable on mobile

**Differentiators vs competition**:
| Feature | Stocky AI | Tickertape | Smallcase |
|---------|-----------|------------|-----------|
| AI chat interface | Yes (4 models) | No | No |
| Multi-agent debate | Yes (3 architectures) | No | No |
| Broker integration | Zerodha + Dhan | View only | Smallcase basket |
| Options analytics | PCR, Max Pain, IV, strategies | Basic | No |
| Real-time news sentiment | 41 feeds + AI | Curated | No |
| Free | Yes | Freemium | Subscription |

**Traction**: 79 commits in 60 days, 20 feature buttons, 31 backend handlers, 27 card components. Live at llm.stockyai.xyz.

## Related Notes
- [[Demo Script]]
- [[Technical Story]]
- [[Numbers]]
