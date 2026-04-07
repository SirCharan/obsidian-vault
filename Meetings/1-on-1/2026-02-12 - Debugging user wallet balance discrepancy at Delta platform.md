---
title: "Debugging user wallet balance discrepancy at Delta platform"
date: 2026-02-12
type: meeting
meeting_type: 1-on-1
project: ""
people:
  []
granola_id: 409413c4-e357-4876-8963-62534756d3a3
granola_url: https://notes.granola.ai/d/409413c4-e357-4876-8963-62534756d3a3
tags:
  - meeting
  - 1-on-1
  - ai
  - trading
status: active
---

### Problem Statement

- User deposited ₹2 lakhs lifetime but only sees ₹1.8 lakhs in UI
- ₹27k discrepancy between expected and displayed balance
- Need to determine if issue is user error or platform bug

### Debugging Approach

- Calculate actual balance using formula:

- Total deposits minus withdrawals
- Plus trading activity (PnL, fees, incentives)
- Minus penalties/liquidation costs
- Cross-reference with internal dashboard data
- Determine if discrepancy is user miscalculation or platform error

### Two Scenarios Analysis

- Scenario 1: User error (actual balance is ₹1.8L)

- Provide breakdown of 4 main heads to support agent
- Support explains inflow/outflow + trading activity to user
- Most problems should resolve with these two main categories
- Scenario 2: Platform error (should show ₹2L)

- Check if backend data is correct vs frontend display issue
- If backend wrong: larger user segment likely affected
- If frontend wrong: API/websocket connection problem

### Support Agent Tools

- Create dashboard showing 4 balance components for any user ID
- Provide total sums rather than individual transaction details
- Enable agents to self-serve common balance inquiries
- For complex cases (margin disputes, liquidations): build trade-specific snapshot system

### Advanced Cases & Compliance

- Margin-related disputes

- May require isolated/cross/portfolio margin details
- Trade-level data access needed for liquidation complaints
- Use publicly available OHLC data when possible
- KYC/AML dashboard requirements

- Track user flow: T0 (signup) → T1 (KYC start) → T2 (KYC complete)
- Monitor drop-off rates between stages
- Focus on reducing abandonment in government verification tools


---
Source: [Granola](https://notes.granola.ai/d/409413c4-e357-4876-8963-62534756d3a3)
