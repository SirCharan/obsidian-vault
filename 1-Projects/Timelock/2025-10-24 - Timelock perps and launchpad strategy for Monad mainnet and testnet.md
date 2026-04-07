---
title: "Timelock perps and launchpad strategy for Monad mainnet and testnet"
date: 2025-10-24
type: meeting
meeting_type: strategy
project: Timelock
people:
  []
granola_id: fb536767-2abe-4d4d-9a9e-028957848d96
granola_url: https://notes.granola.ai/d/fb536767-2abe-4d4d-9a9e-028957848d96
tags:
  - meeting
  - timelock
  - strategy
  - defi
  - crypto
  - ai
  - trading
  - product
status: active
---

### Platform Development Options

- Timelock offers multiple product levels by complexity
- Perps for single coin (simplest implementation)
- Permissionless markets with minimum liquidity requirements (500K-1M)
- Launch pad + perps for all markets
- Binary options and full system (6,000 lines of code, $300K audit)

### Testnet Implementation Plan

- Two-week development timeline for MVP perps
- Meme Steroid collects TROID tokens from community via contract

- Users send tokens, receive rewards/wrapped version
- 20-30% token supply participation expected (minimum 10%)
- Timelock provides USDC pairing from their reserves
- Trading pairs: TROID/USDC on testnet, all fees paid in MON
- Live on memesteroid subdomain, “Powered by Timelock”

### Technical Architecture

- No liquidation, no loss perps using Uniswap liquidity
- Hedging mechanism: borrow from tick, sell if price rises, repay with profit
- Funding rates replace traditional premiums
- Users always retain deposited margin minus funding costs
- Contract audit covered by Timelock’s angel investors

### Mainnet Strategy Pivot

- Original plan: Launch ROID token on external launchpad, then add perps
- New approach: Create separate branded launchpad platform

- Joint venture with new branding (not Meme Steroid or Timelock)
- Purple/white Monad-inspired design
- Separate Twitter account and domain required
- Timelock launchpad advantages:

- 50% swap revenue sharing with creators
- Fair launch, no bonding curves
- Instant perps integration for all launched tokens
- No graduation requirements

### Revenue Sharing Structure

- Testnet: 50/50 split of perp trading fees
- Mainnet launchpad: TBD (25-50% range discussed)
- Audit costs: Covered by Timelock
- Development costs: Each team covers own expenses
- UI/UX: Timelock designer leads with Meme Steroid color scheme input

### Liquidity Requirements & Challenges

- Current TROID liquidity extremely thin (~$1 on Monday Trade)
- Most tokens held by community (90%+), not available for trading
- Mainnet needs substantial liquidity for viable perps
- Minimum $250K token value threshold for permissionless markets
- Meme Steroid only allocating 5% tokenomics to liquidity (insufficient)

### Platform Differentiation

- Timelock vs competitors: No bonding curves, fair launches, instant graduation
- GMX model rejected as flawed (relies on internal oracles)
- Pump.fun success due to first-mover advantage, but has pump/dump issues
- Orderbook/CLOB not viable for meme coins (requires market makers)

### Next Steps

- Contract drafting: Timelock to prepare partnership agreement
- Brand development: Joint brainstorming for launchpad name/identity
- Technical documentation: Simplified docs for Meme Steroid team review
- Timeline: Start testnet development immediately, mainnet planning in parallel
- Decision point: Testnet only if 2+ weeks available for user testing


---
Source: [Granola](https://notes.granola.ai/d/fb536767-2abe-4d4d-9a9e-028957848d96)
