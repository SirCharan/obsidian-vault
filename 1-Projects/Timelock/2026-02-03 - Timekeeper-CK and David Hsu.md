---
title: "Timekeeper/CK and David Hsu"
date: 2026-02-03
type: meeting
meeting_type: 1-on-1
project: Timelock
people:
  - "[[Davidhsu]]"
granola_id: 90c072a0-a9af-4329-bc71-89bc6255d20d
granola_url: https://notes.granola.ai/d/90c072a0-a9af-4329-bc71-89bc6255d20d
tags:
  - meeting
  - timelock
  - 1-on-1
  - defi
  - trading
  - product
status: active
---

### Ether Adventures Overview

- Dave Hsu, GP at Ether Adventures (NYC-based, $20M fund backed by Etherfi)
- Structured like corporate VC with integration/distribution value-add
- Portfolio support through Etherfi: TVL, go-to-market, distribution, day-one protocol usage
- Investment focus: DeFi and financial services
- Fund metrics:

- Closed November 2025, actively deploying
- 5 investments completed
- Average check: $560k (range: $250k-$1M)
- Notable investment: Hyperbeat (co-led with Electric Capital)
- Bullish on Hyperliquid ecosystem

### TimeKeeper Product & Mechanism

- Core thesis: Perps without liquidations using Uniswap-derived pricing

- No external oracles or market makers
- Reduces attack vectors and MEV opportunities
- Built on everlasting options concept (referenced Paradigm/SBF 2021 paper)
- Mechanism overview:

- Borrows ETH from Uniswap pools, holds in escrow
- Price down: Simply repay borrowed ETH (no liquidation)
- Price up: Sell escrowed ETH, repay LP, trader keeps profit
- Unlocks impermanent loss from Uniswap LPs as trader profit
- Current deployment: Live on Monad mainnet (proof of concept)
- Liquidity constraints: 1-5% of pool TVL available for no-slippage trades

- $10B Uniswap TVL could support $500M-$1B open interest
- Key differentiator from Panoptic: Retail-focused “perps without liquidations” vs complex options narrative

### Fundraising & Traction

- Raising: $1.5-2M round
- Current status: $500-600k verbal commitments, seeking $500k-1M more
- Looking for lead investor to price round (targeting Ether Adventures)
- Timeline: Close by end of March 2026
- Previous traction metrics (Monad testnet):

- $7.3M trading volume
- $11.2k fees generated (15 bps fee capture ratio)
- Volume dropped when Monad moved to mainnet
- Next steps: Deploy $20-30k personal capital for MON/USDC pool while fundraising

### Next Steps

- Dave: Review detailed docs, share with technical team for evaluation
- Dave: 2-3 week due diligence process timeline
- Charandeep: Share comprehensive documentation (docs preferred over other formats)
- Charandeep: Deploy additional pool with personal capital
- Charandeep: Target Paradigm for future seed round (too early for pre-seed)

## Related

- [[Davidhsu]]
- [[Timelock]]


---
Source: [Granola](https://notes.granola.ai/d/90c072a0-a9af-4329-bc71-89bc6255d20d)
