---
title: "Scott and Charandeep Kapoor"
date: 2025-08-07
type: meeting
meeting_type: external
project: Timelock
people:
  - "[[Scott]]"
  - "[[Jeff A.]]"
  - "[[Domaditya10]]"
granola_id: 242cbb5f-2576-452e-a42c-63e0923e9257
granola_url: https://notes.granola.ai/d/242cbb5f-2576-452e-a42c-63e0923e9257
tags:
  - meeting
  - timelock
  - external
  - defi
  - crypto
  - ai
  - trading
  - product
status: active
---

### Timelock Overview & Product Strategy

- Building options protocol disguised as “non-liquidable leverage” platform

- Hiding options terminology to avoid crypto user resistance
- Custom duration expiries available
- Starting with ETH/BTC on Monad, expanding multi-chain (avoiding Ethereum due to gas costs)
- Two-sided marketplace model

- LPs deposit into vaults first (supply-side priority)
- Traders buy time locks (options) from LP liquidity
- Using Uniswap IV pricing (~50 IV) vs traditional derivatives (~60-65 IV)

### Vault Management Partnership Opportunity

- UniV3 Vault Manager role - Performance + Management fees structure

- LPs deposit single-sided (USDC/USDT) into vaults
- Vault managers deploy into UniV3 ranges, actively rebalance, auto-compound fees
- Handle liquidity holes when traders borrow from specific ticks
- All vault liquidity fungible across depositors
- Stable vault concept (advanced)

- Hedge UniV3 positions with perps to create delta-neutral stable coin yields
- Targeting 20% APR (UniV3: 20-30%, perps funding: 10%, hedging losses: -5-10%)
- Requires automation of rebalancing + perps hedging

### Trading & Arbitrage Opportunities

- Trading - Custom duration options cheaper than traditional platforms

- Hedge existing option books with long positions on Timelock
- Flexible expiry selection for portfolio management
- Arbitrage potential between Timelock and Deribit

- Buy options on Timelock (~50 IV), sell on Deribit (~60-65 IV)
- Delta-neutral strategies across platforms
- Scott’s background: former biggest Squeeth trader, familiar with vol arbitrage

### Next Steps

- Timelock testnet launch: 1 week
- Documentation & whitepaper: end of this week
- Initial partnership focus: UniV3 vault management on testnet
- Stable vault development: requires mainnet deployment with perps access
- TG group setup for ongoing collaboration discussions
- Letter of intent document needed outlining partnership specifics

## Related

- [[Scott]]
- [[Jeff A.]]
- [[Domaditya10]]
- [[Timelock]]


---
Source: [Granola](https://notes.granola.ai/d/242cbb5f-2576-452e-a42c-63e0923e9257)
