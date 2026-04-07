---
tags:
  - stocky-ai
  - product
  - roadmap
created: 2026-04-07
status: complete
---

# Roadmap

## Near-Term (Next 30 Days)

| Feature | Impact | Complexity |
|---------|--------|-----------|
| **Real-time price streaming** | Biggest retention driver -- live LTP in OverviewCard, PortfolioCard | High (WebSocket infra) |
| **Watchlist dashboard** | View saved stocks with price alerts | Medium |
| **Playwright E2E tests** | Prevent regression cycles (had 4 commits in 11 min reverting each other) | Medium |
| **Push notifications** | Price alerts, earnings reminders via Web Push API | Medium |

## Medium-Term (60-90 Days)

| Feature | Impact | Complexity |
|---------|--------|-----------|
| **Multi-user auth** | Required for any SaaS revenue | High |
| **PostgreSQL migration** | Required for >1 concurrent user | High |
| **Component library** | Extract `@stocky/ui` for consistency | Medium |
| **Semantic intent parser** | Replace brittle regex with vector search | Medium |
| **Options P&L calculator** | Strategy builder with payoff diagrams | High |

## Long-Term (6+ Months)

| Feature | Impact | Complexity |
|---------|--------|-----------|
| **Mobile app** (React Native) | Capture mobile-native UX | Very High |
| **Self-hosted LLM** | Cost reduction at scale, custom fine-tuning | Very High |
| **Paper trading** | Risk-free strategy testing | High |
| **Social features** | Share trades, follow portfolios | High |
| **Algo trading** | Automated strategy execution | Very High |

## Related Notes
- [[Features]]
- [[Scaling Plan]]
- [[Tradeoffs]]
