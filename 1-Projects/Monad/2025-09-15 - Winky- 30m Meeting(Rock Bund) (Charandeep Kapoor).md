---
title: "Winky: 30m Meeting(Rock Bund) (Charandeep Kapoor)"
date: 2025-09-15
type: meeting
meeting_type: 1-on-1
project: Monad
people:
  - "[[Winky Zhao]]"
  - "[[Jeff Chu]]"
granola_id: f772492c-5fa7-4e96-9181-a13f8c647624
granola_url: https://notes.granola.ai/d/f772492c-5fa7-4e96-9181-a13f8c647624
tags:
  - meeting
  - monad
  - 1-on-1
  - defi
  - crypto
  - ai
  - trading
  - product
status: active
---

### Time Lock Product Overview

- Building oracle-less, liquidation-free leverage trading mechanism
- Borrows idle tick liquidity from Uniswap V3 pools to create option-like payoffs
- Pricing formula derives implied volatility from Uniswap V3 pools

- 15-20% lower than Deribit’s implied volatility
- Native crypto mechanism vs traditional order book systems
- Currently live on Monad testnet with 300+ traders tested

### Vault Structure and Mechanics

- Two vault types offered:

- Uniswap V3 Vaults - LP earns Uniswap payoff + trader premiums + swap fees
- Stable Vaults - Delta neutral via short perpetuals on perp DEXs
- Liquidity deployment strategy:

- 70% tight narrow range (can be borrowed)
- 20% wider range
- 10% full range
- Protocol has exclusive borrowing rights, not vault managers

- Immutable contracts with minimal governance
- Only protocol can withdraw/swap/repay liquidity

### Partnership and Collaboration Options

- Three collaboration models presented:

- USDC liquidity provider - No lockups, withdraw anytime

- Projected 15-24% yields from trader premiums + swap fees + funding rates
- Can offer 12% fixed return if preferred
- Vault manager - Create own pools, manage liquidity

- Keep all swap fees, earn extra from inorganic trading demand
- Optional borrowing allowance for additional trader premium yield
- VC investment - $1.5M raise at $12-15M valuation

- 10-12% equity dilution, flexible on SAFT vs priced round

### Security and Risk Management

- Jeff’s primary concern: Asset security and fund control
- Protocol-only withdrawal rights from escrow accounts
- Vault managers can only trigger rebalances, not withdraw user funds
- All transactions atomic - LP always fully collateralized
- Traders bear slippage/swap fee risks, not LPs
- Maximum trade duration: 1 day

### Next Steps

- Jeff to review internally with VC team for investment consideration
- Charandeep to send detailed documentation:

- VC deal terms and pitch deck
- USDC liquidity provision details
- Post-Monad mainnet launch: Discuss liquidity provisioning and vault management
- Potential follow-up at Token2049 conference
- Arbitrum expansion planned after Monad deployment

## Related

- [[Winky Zhao]]
- [[Jeff Chu]]
- [[Monad]]


---
Source: [Granola](https://notes.granola.ai/d/f772492c-5fa7-4e96-9181-a13f8c647624)
