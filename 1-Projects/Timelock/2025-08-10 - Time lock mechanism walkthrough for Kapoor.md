---
title: "Time lock mechanism walkthrough for Kapoor"
date: 2025-08-10
type: meeting
meeting_type: 1-on-1
project: Timelock
people:
  []
granola_id: 2d08b41b-cb77-44e1-ac39-aa21ac323d2b
granola_url: https://notes.granola.ai/d/2d08b41b-cb77-44e1-ac39-aa21ac323d2b
tags:
  - timelock
  - meeting
  - 1-on-1
  - defi
  - trading
status: active
---

### Time Lock Core Mechanism Overview

- Time Lock combines two protocols: Strike (trading mechanism) and Orange Finance (automated vaults)
- Enables traders to achieve 1000x leverage without liquidation risk through borrowing Uniswap v3 liquidity
- Key innovation: Position always fully collateralized regardless of price movement

- Protocol holds ETH in escrow outside Uniswap pool
- LP gets expected payoff whether price goes up or down
- No liquidation needed since collateral always covers borrowed amount

### Trading Mechanics Deep Dive

- Long positions: Borrow next tick above current price

- If price rises, protocol swaps ETH for USDC, repays LP, trader gets profit
- If price falls, protocol returns original ETH to LP, trader loses nothing
- Payoff structure creates asymmetric risk/reward

- Traders capture full upside when right
- Zero downside when wrong (unlike traditional leverage)
- Linear payoff advantage over competitors like Panoptic (curved payoff makes hedging difficult)

### Vault Structure & LP Incentives

- Two vault types planned:

- Uniswap v3 vaults - retain standard uni v3 payoff + trader premiums
- Stable vaults - hedge uni v3 exposure via perps for stable coin returns
- LP incentives beyond normal uni v3 returns:

- Automated liquidity management (Orange Finance functionality)
- Trader premium payments
- Projected 20-27% yield combining swap fees, trader premiums, funding rates
- Strategy curators (like STS Digital) earn performance fees for vault management

### Current Development Status & Blockers

- Live on Tenderly testnet, need Monad testnet deployment for ecosystem funding
- 70% of debugging complete, mint position integration remaining
- Front-end ready, just needs contract address updates
- Kapoor joining team to help complete mint position functionality and overcome deployment blockers
- Target: 9-month timeline for token launch and public raise

### Next Steps

- Kapoor to review mechanism video and documentation
- Vedant to walk Kapoor through existing codebase and mint position implementation
- Deploy static range liquidity on Monad testnet (no automated rebalancing initially)
- Complete tick borrowing functionality to enable first live product


---
Source: [Granola](https://notes.granola.ai/d/2d08b41b-cb77-44e1-ac39-aa21ac323d2b)
