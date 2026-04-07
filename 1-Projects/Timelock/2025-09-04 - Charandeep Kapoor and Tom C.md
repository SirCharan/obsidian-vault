---
title: "Charandeep Kapoor and Tom C"
date: 2025-09-04
type: meeting
meeting_type: 1-on-1
project: Timelock
people:
  - "[[Tom]]"
  - "[[Chat]]"
granola_id: e64ffa5a-ae8f-4cb4-8f5f-00c7aaea11f5
granola_url: https://notes.granola.ai/d/e64ffa5a-ae8f-4cb4-8f5f-00c7aaea11f5
tags:
  - meeting
  - timelock
  - 1-on-1
  - defi
  - ai
  - trading
  - product
status: active
---

### TimeL0ck Product Overview

- Borrows Uniswap V3 tick liquidity and escrows assets outside pool to prevent automatic swaps
- Creates fully collateralized, non-liquidable, non-liable trading positions
- Enables options trading on any asset with Uniswap V3 pool (including meme coins)
- Current product variants:

- TimeL0ck Trade: Custom duration at-the-money calls/puts with upfront premium
- TimeL0ck Perps: Perpetual options with continuous funding rate
- TimeL0ck Options: OTM options (roadmap)

### Strategy Arbitrage & Pricing Model

- Identified 20-25% arbitrage opportunity between TimeL0ck and Deribit

- Uniswap V3 LPs earn 0.75-0.8 BSM vs 1.0 BSM on traditional options
- Long calls on TimeL0ck, short calls on Deribit captures spread
- Premium calculation based on implied volatility formula: 2 × fee rate × volume / √tick liquidity
- Maximum outperformance over standard LP strategies: 500%
- Current capacity: 0.1 ETH trade size from 10 ETH TVL (0.5-1% ratio without slippage)

### Partnership Structure with Tom/Trombone

- TimeL0ck seeks vault managers offering different alpha strategies
- Trombone’s asymmetrical limit orders + leftover limit orders would provide continuous LP supply
- Revenue model for Trombone:

- Keep existing performance fees on swap fees
- Add performance fees on trader premiums
- TimeL0ck takes no cut from LPs
- Key constraint: Borrowed tick liquidity cannot be rebalanced until positions close
- Withdrawal cooldowns: Maximum 1-day positions require cooldown periods

### Next Steps

- Tom to review integration docs from Apoor
- Partnership discussions to continue via Telegram
- Potential day-one launch on Monad mainnet (waiting for subgraph infrastructure)
- Delta neutral stablecoin vault discussion scheduled for next call

## Related

- [[Tom]]
- [[Chat]]
- [[Timelock]]


---
Source: [Granola](https://notes.granola.ai/d/e64ffa5a-ae8f-4cb4-8f5f-00c7aaea11f5)
