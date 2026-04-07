---
title: "Timelock PNL calculation and uniswap liquidity borrowing strategy review with team member"
date: 2025-08-18
type: meeting
meeting_type: strategy
project: Timelock
people:
  []
granola_id: 45320164-7025-47c8-83dc-748a3ef7d9b0
granola_url: https://notes.granola.ai/d/45320164-7025-47c8-83dc-748a3ef7d9b0
tags:
  - meeting
  - timelock
  - strategy
  - defi
  - ai
  - product
status: active
---

### Settlement Engine Logic Migration

- Function moved from JavaScript to Solidity for easier implementation
- Iterates through all positions for each option (not single positions)
- Calculates profit for each position - adds to total if above zero, ignores otherwise
- Liquidity stored in Uniswap units

- One position’s liquidity converts to specific amounts of each asset
- Naming conventions unclear but logic sound

### PnL Calculation and Price Mechanics

- Current system doesn’t account for premium in PnL calculations

- Dopex also excludes premium from PnL
- Any profit above $1 worth claiming regardless of premium paid
- Negative PnL display is intentional design choice

- Shows what loss would be on other platforms
- TimeLog prevents actual losses beyond premium
- Borrowing mechanics require taking from next available tick

- All ticks above current price contain ETH
- All ticks below current price contain USDC
- Current tick contains both assets
- Similar to order book slippage on other platforms

### Technical Deployment Readiness

- Testnet deployment nearly complete
- Required changes before going live:

- Remove mint function
- Add link to Monad faucet where “Monad Testnet” appears
- Wallet connection automatically switches to Monad testnet
- TradingView integration not loading (hardcoded values still present)
- Fee tracking system needs improvement

- Current system proportionally divides fees among all LPs
- Should track deposit timing for accurate fee allocation
- Need to account for: Uniswap fees, ETH/USDC price changes, trader premiums

### Strategic Vision: Yield-Bearing Stablecoin

- Opportunity to build on TimeLog’s unique position
- Development sequence:

- Complete current platform
- Build auto-rebalancing vaults
- Partner with market makers like STS Digital
- Create wrapped stablecoin product
- Revenue sources for yield product:

- 20-25% APY from Uniswap fees (±10% pools)
- 5% additional from funding rates (assuming 50% ETH exposure, 10% funding)
- Market opportunity significant

- Ethena: $11.35B TVL at 8% yield
- Basis trading protocols reaching $100M TVL in 2-3 months
- High demand from capital holders seeking 8-10% stable returns
- Competitive advantage: unique liquidity borrowing mechanism creates high barrier to entry

### Next Steps

- Complete minor UI changes and coordinate with Vedanta for final testnet review
- Schedule 5pm call with Abdullah (Head of DeFi) and CJ (Head of Ecosystem) from Monad
- Resolve Telegram spam issues to add team member to Monad group
- Begin documentation and whitepaper development
- Target $800k fundraise and $100k Monad Foundation grant (minimum $10M valuation)


---
Source: [Granola](https://notes.granola.ai/d/45320164-7025-47c8-83dc-748a3ef7d9b0)
