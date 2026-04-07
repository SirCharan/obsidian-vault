---
title: "Michael Mullaney and Timekeeper Timelock"
date: 2025-11-25
type: meeting
meeting_type: external
project: Timelock
people:
  - "[[Michael]]"
  - "[[Paolo]]"
  - "[[Fred from Fireflies]]"
granola_id: 703be2d8-8464-4117-9f1a-fd9638420bf5
granola_url: https://notes.granola.ai/d/703be2d8-8464-4117-9f1a-fd9638420bf5
tags:
  - meeting
  - timelock
  - external
  - ai
  - product
status: active
---

### Octane Security Overview

- AI-powered security product that plugs into GitHub for protocol reviews
- Works with major ecosystems: Monad, Uniswap, Circle, Avalanche
- Pre-deployment security checks for teams before going live
- In development since 2023, regularly catches issues missed by manual reviews

### AI vs Traditional Audit Comparison

- Octane currently complements, not replaces traditional audits

- Still recommend tier-1 firms (TOB, Halborn) for novel tech/new chains
- Catches different vulnerabilities than manual auditors
- Example: Found high vulnerability in stablecoin protocol (30 minutes) that 5 tier-1 auditors missed

- Vulnerability was 13 contract dependencies deep
- Would take manual auditor 2+ days to map
- Specifically found Panoptic vulnerability before public disclosure

- V3 model releasing next week with stronger capabilities

### Timekeeper Protocol Context

- Building liquidation-free perpetual platform
- 4,000-6,000 lines of code across 5-6 repositories
- Using Uniswap liquidity for fully collateralized positions without liquidations
- “Everlasting options as perpetuals” approach
- Similar to Panoptic (who got hacked despite 6 audits)

### Pricing & Monad Partnership

- One-time vulnerability scans fully covered by Monad

- Includes all repositories (5-6 repos with 4K-6K lines)
- No cost to Timekeeper
- Ongoing subscription pricing based on:

- Number of seats (scan ability + platform access)
- Number of repositories
- Covers economic vulnerabilities, business logic, code inefficiencies

### Next Steps

- Charandeep’s CTO to complete scope form (30-60 minutes)

- Repository details, commit hashes, branch names
- Technical details, external dependencies
- Background on codebase
- Form submission by tomorrow
- Follow-up call Friday or Monday next week (US holiday Thursday)
- Timekeeper will highlight 3-4 specific edge cases for emphasis
- Octane will provide vulnerability report within 48-72 hours

## Related

- [[Michael]]
- [[Paolo]]
- [[Fred from Fireflies]]
- [[Timelock]]


---
Source: [Granola](https://notes.granola.ai/d/703be2d8-8464-4117-9f1a-fd9638420bf5)
