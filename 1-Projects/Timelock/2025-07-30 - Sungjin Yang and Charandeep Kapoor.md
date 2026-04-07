---
title: "Sungjin Yang and Charandeep Kapoor"
date: 2025-07-30
type: meeting
meeting_type: 1-on-1
project: Timelock
people:
  - "[[Yjake345]]"
granola_id: f2bb59ae-675c-46c5-8a1a-30197413f1f9
granola_url: https://notes.granola.ai/d/f2bb59ae-675c-46c5-8a1a-30197413f1f9
tags:
  - meeting
  - 1-on-1
  - defi
  - crypto
  - ai
  - trading
status: active
---

### Time Lock Trading Protocol Overview

- Leveraged trading for any ERC-20 token using borrowed UniSwap v3 LP liquidity

- Not limited to order books or peer-to-pool mechanisms like GMX
- Borrows tick liquidity from UniSwap v3 LPs to create positions
- Enable leverage for any token with UniSwap v3 pool (or can create pool)
- Currently live on Base mainnet, testnet deployment pending
- Solves meme coin derivatives gap

- Less than 1% of meme coins evolve to have perps
- 99%+ pump.fun tokens are pump-and-dump due to zero commitment cost
- Can enable derivatives from day zero after graduation

### Technical Mechanism & Business Model

- Borrows specific ticks from UniSwap v3 pools, holds outside pool during trades

- Example: Long ETH position borrows next tick, protocol holds 1 ETH
- If ETH rises to $5,000, protocol swaps for $5,000 USDC, repays LP $3,500
- Trader keeps profit, no active market makers or oracles needed
- LP limitations: 5-10% of pool size available for leverage trades

- 100k liquidity pool → 5-10k worth of trading capacity
- Revenue model:

- LPs earn premiums (e.g., 6 USDC/hour for 1 ETH long) plus trading fees
- Time Lock charges additional trading fees + performance fees on managed vaults
- All trades are non-liquidatable, oracle-free, governance-free protocol

### Partnership Opportunity with pump.fun

- Instead of burning LP tokens after bonding curve graduation, transfer NFT to Time Lock

- Enables immediate derivatives trading for graduated tokens
- Protocol revenue sharing possible since LP tokens typically burned anyway
- Benefits for meme coin ecosystem:

- Users can short suspected scams (currently only buy-side possible)
- Price discovery through derivatives creates fair market pricing
- Filters out scam projects through market mechanisms
- Next steps:

- Sungjin to review with dev team (non-technical founder needs dev input)
- Time Lock documentation completion in 2-3 days
- Continue discussion via Telegram group with both teams
- Consider perps development if partnership proceeds (currently only timed trades live)

## Related

- [[Yjake345]]


---
Source: [Granola](https://notes.granola.ai/d/f2bb59ae-675c-46c5-8a1a-30197413f1f9)
