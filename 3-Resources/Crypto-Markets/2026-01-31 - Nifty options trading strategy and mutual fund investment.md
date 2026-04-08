---
title: "Nifty options trading strategy and mutual fund investment approaches"
date: 2026-01-31
type: meeting
meeting_type: strategy
project: ""
people:
  []
granola_id: f95cf8c6-aa82-4fe9-acd6-056031a738d9
granola_url: https://notes.granola.ai/d/f95cf8c6-aa82-4fe9-acd6-056031a738d9
tags:
  - crypto-markets
  - meeting
  - strategy
  - trading
status: active
---

Trading Strategy Discussion & Adjustments
- Current covered call strategy on Nifty (2 lots) not performing well
- Zero returns after 4 months - pattern of losing all profits in 5th month
- Selling 25,400 strike calls monthly for ~26,000 premium
- Major downside risk: loses money on both call options (when Nifty rises) and Nifty Bees (when Nifty falls)
- Strategy adjustment techniques based on time to expiry:
- Less than 7 days: Sell ATM put option
- Reduces loss by 150-200 points if Nifty continues rising
- Simple one-input trade decision7-20 days: Sell OTM straddle
- Requires predicting approximate Nifty target (e.g., 25,700)
- Provides flat profit zone but more complex (two inputs to consider)
- More than 20 days: Two options available
- Conservative: Add bull call spread (buy 450c, sell 850c)
- Reduces profit from 355 to ~165 points but very safe upside
- Breakeven moves from 25,755 to 25,900
- Aggressive: Sell additional call option (ratio spread)
- Preserves original 23,000 profit but doubles upside risk
- Slope changes from -1 to -2 (lose ₹130 per point vs ₹65)

### Alternative Trading OpportunitiesBTC options on Delta Exchange mentioned but not explored in detail
- Mutual fund strategy discussion:
- Currently investing in index funds (Nifty 50, Next 50, Mid Cap 150)
- Shared previous sector rotation strategy using AI signals
- Achieved 60-70% returns, top 1% performance on ET Money

### Used ChatGPT 3.5 to analyze sector parameters (FII flows, block deals, P/E ratios)
- Strategy focused on sectoral funds vs broad index approach
- Gold/silver ETFs mentioned as current holdings
- Platform & Algo Trading Interest
- Expressed interest in algo trading platforms and webinars
- Currently exploring Algo
- Test but facing slippage issues
- Wants to be included in any upcoming webinars or educational content
- Previous crypto trading experience on Delta Exchange
- Built trading bot features for Delta
- Stopped due to liquidation risks and high leverage concerns
- Commodities trading background (MCX)
- Previous experience with gold/silver futures
- Managed positions using stop losses and circuit limits

---
Source: [Granola](https://notes.granola.ai/d/f95cf8c6-aa82-4fe9-acd6-056031a738d9)
