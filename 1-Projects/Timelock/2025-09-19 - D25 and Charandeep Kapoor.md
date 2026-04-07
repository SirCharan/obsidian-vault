---
title: "D25 and Charandeep Kapoor"
date: 2025-09-19
type: meeting
meeting_type: 1-on-1
project: Timelock
people:
  - "[[Dagavrikov]]"
  - "[[Chat]]"
granola_id: 3d934a67-1f4a-4667-99d6-a65d7e8b5599
granola_url: https://notes.granola.ai/d/3d934a67-1f4a-4667-99d6-a65d7e8b5599
tags:
  - meeting
  - timelock
  - 1-on-1
  - defi
  - crypto
  - ai
  - trading
  - product
status: active
---

### Time Lock Product Demo

- Currently live in closed beta with WMON/WETH pairs on testnet
- No-loss perpetual trading mechanism

- Traders pay only premium upfront (e.g., $0.38 for $33 trade)
- No liquidations based on price movements
- Trades close only when funding fees exceed margin or duration expires
- Live demonstration of 78x leverage long position on WMON

- $33 notional size for $0.38 premium
- Can simultaneously go long and short same token

### Proposed Integration with GMoon

- Add pro/retail switcher to current interface

- Retail: existing buy/sell functionality
- Pro: long/short positions with fixed leverage options
- Fixed 5x leverage for simplicity (1 MON margin for 5 MON notional)
- Revenue split: 50/50 on funding fees collected

- GMoon keeps 100% of swap fees
- Better terms than other partnerships (60/40 or 90/10 planned)

### Technical Concerns & Resolution

- GMoon worried about liquidity borrowing affecting token prices
- Time Lock explanation:

- Borrowing tick liquidity doesn’t change pool price (only swaps do)
- Maximum 30% of any tick can be borrowed
- Limited to 5-10 ticks from current price
- 70/30 liquidity deployment ratio maintained
- Trade size limitations prevent complete tick depletion
- Arbitrage opportunities minimal due to symmetric tick effects

### Next Steps

- GMoon needs 2-3 days to review documentation and discuss internally
- Decision on partnership commitment within 2 days
- Time Lock seeking first meme coin launchpad partner before Token2049 (10 days)
- Technical integration timeline dependent on GMoon’s CTO availability
- Continued discussion in group chat for questions

## Related

- [[Dagavrikov]]
- [[Chat]]
- [[Timelock]]


---
Source: [Granola](https://notes.granola.ai/d/3d934a67-1f4a-4667-99d6-a65d7e8b5599)
