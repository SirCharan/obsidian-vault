---
title: "Timekeeper / CK and James Hunsaker"
date: 2025-10-22
type: meeting
meeting_type: 1-on-1
project: Timelock
people:
  - "[[Jhunsaker]]"
  - "[[Chat]]"
granola_id: fc59e13f-e718-4bed-8c41-6e5b33fda409
granola_url: https://notes.granola.ai/d/fc59e13f-e718-4bed-8c41-6e5b33fda409
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

### Product Overview & Mechanism

- TimeKeeper built on custom derivative borrowing from Uniswap V3 liquidity

- Options-like payoff with no option seller - LPs remain risk neutral
- Traders can profit when right, but face no loss when wrong
- Native IV calculation from Uniswap rather than external oracles
- Two live products:

- TimeKeeper Trade - at-the-money calls/puts with custom durations (1 hour to 7 days)
- TimeKeeper Options (beta) - custom strike prices at any tick, custom expiry down to seconds
- Planned TimeKeeper Perps - perpetual options paying only funding, no liquidation risk

### Technical Architecture & Innovation

- Entirely built on Uniswap V3 infrastructure

- Borrows idle liquidity from pools for trades
- Pricing derived from Uniswap’s liquidity distribution and volume
- No market makers or external oracles required
- Gas optimization challenges remain for on-chain IV calculation

- Currently using off-chain oracle for IV updates
- Working on reducing transaction costs for retail users
- Enables trading on any asset with Uniswap V3 pool

- Permissionless market creation
- Even meme coins without oracles/market makers become tradable

### Fundraising Challenges & Status

- Team of 4 core members, started 2 years ago with $100K personal funds
- Down to last $20-25K, need funding for audits ($15-40K range)
- VC feedback issues:

- Most VCs want token launch timeline (6-12 months)
- Team prefers 2-3 year development approach
- VCs comparing to existing perp DEXs rather than understanding novel mechanism
- Difficulty explaining complex derivative mechanics to junior analysts
- Seeking $1.5-2M for 2-year runway

- $250-300K angel commitments contingent on lead VC
- Angels won’t lead round themselves

### James Hunsaker’s Feedback & Advice

- Strong conviction on avoiding rushed token launch

- “If they want you launch a token, that’s because they want to sell the token”
- Longer runway before fundraising = better valuation and VC terms
- Product direction recommendations:

- Focus on retail UX over institutional features initially
- Launch scrappy version to gain traction before iterating
- Binary options/prediction markets could drive retail adoption
- Meme coin shorting capability unique value proposition
- Audit pathway: Can launch with current TimeKeeper Trade product in 15-20 days post-audit

### Next Steps

- James to review pricing documentation and pinned article
- James to connect with relevant people for VC introductions
- Team considering:

- Meme coin launchpad with single LP model
- Uniswap Foundation meeting scheduled this week
- Delaware C-corp formation pending cap table decisions
- Multi-chain expansion strategy for larger assets

## Related

- [[Jhunsaker]]
- [[Chat]]
- [[Timelock]]


---
Source: [Granola](https://notes.granola.ai/d/fc59e13f-e718-4bed-8c41-6e5b33fda409)
