---
title: "Options protocol fee structure and settlement strategy planning"
date: 2025-11-27
type: meeting
meeting_type: strategy
project: Timelock
people:
  []
granola_id: 1e4df7e4-1ee1-4201-bc12-b34a35611dc8
granola_url: https://notes.granola.ai/d/1e4df7e4-1ee1-4201-bc12-b34a35611dc8
tags:
  - meeting
  - strategy
  - ai
  - trading
status: active
---

### Protocol Fee Structure

- Two fee components implemented:

- Opening fee: 0-1% charged once when opening position (0.5% recommended)
- Base fee: Percentage of premium charged continuously
- Both fees go to protocol, not shared with LPs
- Opening fee bypass when protocol down and options expire

- Simple to implement - can toggle on/off easily
- Fee split strategy:

- 50/50 split achievable with 100% base fee rate
- Scalable to 60/40 or other ratios by adjusting base fee vs premium ratio
- Display combined rate as single “funding rate” for user clarity

### Settlement Engine Downtime Protocol

- Maximum downtime: 6 hours, minimum: 1 hour expected
- No opening fee charged when protocol down and positions expire
- Current bot reliability issues when gas runs out
- Decentralized settlement option discussed:

- Open source 120-line settlement code
- Fixed reward (110-120 gas units) for closing trades
- Protocol revenue funds rewards when main bot down
- 99.9% uptime achievable with proper gas management

### Gas Optimization Strategy

- Immutable variables vs mutable approach:

- Reading cost: 2k units (8k on Monad)
- Contract redeployment breaks even after 10-15 trades
- Recommended: Use immutable model for established pairs
- Experimental phase: Test 2-3 pairs, then set permanent rates

### Admin Panel Implementation

- Front-end admin panel completed
- Four key variables configured:

- Opening fee (min/max)
- Base fee rate
- Premium calculations
- Pair-specific settings
- Ready for meme coin product launch with quick pair additions

### Technical Architecture

- Settlement engine: 120 lines of code, no external dependencies
- Premium calculation separate from protocol fees
- Base fee applies every funding period
- Opening fee one-time charge only
- Contract redeployment strategy finalized for fee updates


---
Source: [Granola](https://notes.granola.ai/d/1e4df7e4-1ee1-4201-bc12-b34a35611dc8)
