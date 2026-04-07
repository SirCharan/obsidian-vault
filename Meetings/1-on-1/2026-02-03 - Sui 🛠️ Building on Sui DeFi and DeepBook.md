---
title: "Sui 🛠️ Building on Sui DeFi and DeepBook"
date: 2026-02-03
type: meeting
meeting_type: 1-on-1
project: ""
people:
  []
granola_id: c467f68e-8f24-4c2b-8d5f-3ce1cd25f7ac
granola_url: https://notes.granola.ai/d/c467f68e-8f24-4c2b-8d5f-3ce1cd25f7ac
tags:
  - meeting
  - 1-on-1
  - defi
  - crypto
  - ai
  - trading
  - product
status: active
---

### Sui Blockchain Architecture Overview

- Object-centric model vs EVM account-based model

- No blocks competing for transaction inclusion
- State consists of objects in different locations
- Transactions mutate objects in state
- Parallelism and scalability advantages

- Transactions on different objects don’t compete
- Example: SUI/USDC pool trades don’t interfere with DEEP/USDC pool trades
- Parallel sequencing without restrictions when objects don’t touch

### DeepBook Features and Structure

- Fully on-chain central limit order book

- Time and price matching for orders
- Each trading pair is its own shared object (e.g., SUI/USDC pool)
- Current SUI/USDC market data:

- Price: $1.13
- Best ask: $1.1313
- Best bid: $1.1309
- Spread: ~3 basis points (0.4 cents)
- Fee structure includes taker fee, maker fee, and stake requirements

- Staking DEEP tokens reduces taker fees and provides maker rebates

### DeepBook SDK Workshop Structure

- Three example files planned:

1. Reading order book for SUI/USDC (completed)
2. Swap functionality (main focus)
3. Additional example
- Workshop client is wrapper around DeepBook SDK

- Added extra functions and logging
- Calls underlying SDK with enhanced output
- Level 2 order book depth configurable (showed 10 ticks above/below mid price)

### Integration and Usage

- DeepBook core completely isolated and independent
- Same order book used by DeepMargin protocol
- All participants place orders in unified system:

- Direct DeepBook core users
- Margin protocol borrowers
- Aggregators routing through DeepBook
- No separate order books for different protocols


---
Source: [Granola](https://notes.granola.ai/d/c467f68e-8f24-4c2b-8d5f-3ce1cd25f7ac)
