---
title: "Time lock product GTM strategy with Anupam and Anshul"
date: 2025-07-20
type: meeting
meeting_type: strategy
project: ""
people:
  []
granola_id: be08e20f-1b99-4e6a-bdf2-692a4d0968ec
granola_url: https://notes.granola.ai/d/be08e20f-1b99-4e6a-bdf2-692a4d0968ec
tags:
  - meeting
  - strategy
  - defi
  - crypto
  - ai
  - trading
  - fundraising
  - product
status: active
---

### Project Overview: Time Lock

- Time lock is a liquidation-free leverage trading DEX

- Built on Uniswap v3 liquidity
- Currently deployed on tenderly fork of Base Mainnet
- Going live on Monarch testnet in 1 week
- Trader front end is live, LP front end coming in 2-3 weeks
- Features: oracle-less, governance-free, no reliance on market makers
- Mechanism details:

- Borrows liquidity from Uniswap v3 LP positions
- Vault managers deploy LP deposits into Uniswap v3
- For long trades: borrows from ticks above current price
- For short trades: borrows from ticks below current price
- Positions are fully collateralized and non-liquidatable

### GTM Strategy & Fundraising

- Current fundraising goal: $1.5-2M

- Initial focus on Monad ecosystem (showing strong interest)
- Need to deploy on testnet first to access Monad’s VC network
- Considering angel round before main fundraising
- Product positioning options:

- Protocol launchpad: enable leverage for any token from day zero
- Multiple trading interfaces:

- Web interface
- Telegram bot integration
- Twitter-based trading commands
- Potential webhook integration with news sources (FOMC events, etc.)
- Alternative ecosystem options:

- MegaEat ecosystem - could position well for their HFT focus
- Polygon already approached but they don’t lead investments
- Need to consider ecosystem fit vs independence

### Risk Management & Product Roadmap

- Anshul suggested Python simulations for risk modeling:

- Optimize parameters like tick selection
- Model economic risks beyond standard protocol risks
- Determine optimal upper/lower bounds for maximum profitability
- Future product development:

- Leverage current codebase to build options and perpetuals
- Build custom durations for specific events (FOMC meetings)
- Create “tap and trade” casino-style interface for retail users
- Develop AI-managed vaults with “20% risk-free APR paid in USDC” narrative

### Next Steps

- Meet IRL to discuss GTM and fundraising strategy
- Set up call with dev team for Python simulation
- Consider application to outlier accelerator program
- Review and analyze Neutral.trade interface
- Evaluate Vietnam blockchain week (Aug 1-2) for relevance
- Don’t miss current fundraising cycle - critical timing window


---
Source: [Granola](https://notes.granola.ai/d/be08e20f-1b99-4e6a-bdf2-692a4d0968ec)
