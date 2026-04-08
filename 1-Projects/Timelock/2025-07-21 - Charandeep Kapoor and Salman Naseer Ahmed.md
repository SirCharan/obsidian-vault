---
title: "Charandeep Kapoor and Salman Naseer Ahmed"
date: 2025-07-21
type: meeting
meeting_type: 1-on-1
project: Timelock
people:
  - "[[Salman Naseer]]"
  - "[[Gautham Santhosh]]"
granola_id: 608190cc-a530-423e-b731-dc767fce8c93
granola_url: https://notes.granola.ai/d/608190cc-a530-423e-b731-dc767fce8c93
tags:
  - timelock
  - meeting
  - 1-on-1
  - defi
  - ai
  - trading
status: active
---

### Time Lock Project Overview

- Building liquidation-free leverage trading platform using unique mechanism

- Borrowing tech liquidity from Uniswap v3 LPs to create fully collateralized positions
- Can offer leverages as high as 1000x
- Currently deployed on Tenderly forked Base mainnet
- ~250-300 users have connected to the demo
- Main difference from Polynomial: not using orderbook or peer-to-pool mechanism

### Technical Mechanism

- Borrowing ETH from Uniswap v3 LP positions and putting it into Protocol escrow

- Example: If ETH price moves from $3,500 to $5,000, protocol holds 1 ETH worth $5,000
- Protocol can swap for 5,000 USDC, repay 3,500 to LP, remainder becomes trader P&L
- Trades are always fully collateralized - LPs are always made whole
- Similar approach to Panoptic and Infinity Pools but with key differences:

- Time Lock can offer linear payoffs (Panoptic can’t)
- Time Lock offers liquidation-free leverage for entire trade duration (Infinity Pools only offers 1hr or 4hr)

### Current Status

- Team of 5 people (Charandeep + 4 hired)
- Building full-time since Nov 2022 (~7-8 months)
- In discussions with Monad

- Monad wants deployment on their testnet
- Monad assigned 7 engineers to work with Time Lock team
- Possible central play around Time Lock protocol
- Current wait list has ~20-30 users signed up

### Business Strategy Discussion

- Polynomial team suggested working with Fluid instead of Uniswap

- “Fluid will overtake Uniswap in market share in 2-3 months”
- “It’s very hard to work with Uniswap. They won’t even retweet you.”
- Salman offered to connect Charandeep with Fluid team
- LP strategy to offer 15-20% delta neutral yield on any token

- Yield management through vault managers (market makers, KOLs, AI agents)
- Potential target: family offices in Dubai seeking 12-15% stable yield

### Fundraising Strategy

- Critical immediate priority is fundraising for audit and development

- “Regarding GTM strategy, I think the main pitch is going to be that we can offer 15-20% neutral yield”
- Salman’s advice on fundraising approach:

- Start with angels before VCs
- Get Delta Exchange founders as angels for credibility
- Focus exclusively on fundraising: “A founder’s job is to raise money and hire a good team”
- Get 5+ angels who can network to VCs
- Consider ecosystem grants from Arbitrum/Monad for audit funding

### Product Enhancement Ideas for Polynomial

- Salman asked for suggestions to improve Polynomial
- Charandeep’s recommendations:

- Implement social/copy trading with Twitter KOLs
- Create orders based on indicators (e.g., RSI value, IV changes)
- Add percentage-based orders (stop loss at 10% down rather than specific price)
- Implement DCA features (buy orders at 5% or 10% drops)

### Next Steps

- Charandeep to send pitch deck to Salman
- Salman to send test funds for Charandeep to try Polynomial
- Charandeep to reconnect with Delta Exchange founders for potential angel investment
- Charandeep to focus on fundraising for next 1-2 months

- “If I can’t raise in this bull market, I won’t be able to raise in the bear”
- Salman offered position at Polynomial if Time Lock doesn’t work out

## Related

- [[Salman Naseer]]
- [[Gautham Santhosh]]


---
Source: [Granola](https://notes.granola.ai/d/608190cc-a530-423e-b731-dc767fce8c93)
