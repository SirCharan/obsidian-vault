---
tags:
  - stocky-ai
  - product
  - frontend
created: 2026-04-07
status: complete
---

# Cards

> [!info] 27 card components dynamically imported in MessageBubble.tsx

## Card Component List

| Component | File | Data Shape |
|-----------|------|-----------|
| **AnalysisCard** | `AnalysisCard.tsx` | Stock fundamentals + technicals + AI verdict + Stocky Score |
| **DeepResearchCard** | `DeepResearchCard.tsx` | Gemini 2.5 Pro deep research output |
| **AgentDebateCard** | `AgentDebateCard.tsx` | Triad/Crew debate result (bull/bear/synthesis) |
| **CouncilProgressCard** | `CouncilProgressCard.tsx` | Real-time Council debate progress (9 steps) |
| **CouncilResultCard** | `CouncilResultCard.tsx` | Final Council verdict + confidence score |
| **DebateProgressCard** | `DebateProgressCard.tsx` | Real-time Triad/Crew progress |
| **OverviewCard** | `OverviewCard.tsx` | Market indices, breadth, gainers/losers |
| **PriceCard** | `PriceCard.tsx` | Single stock price lookup |
| **NewsCard** | `NewsCard.tsx` | Aggregated RSS news with sentiment |
| **MacroCard** | `MacroCard.tsx` | Macro indicators dashboard |
| **FiiDiiCard** | `FiiDiiCard.tsx` | FII/DII flow data visualization |
| **TopStocksCard** | `TopStocksCard.tsx` | Multi-category top stocks dashboard |
| **ChartCard** | `ChartCard.tsx` | TradingView chart embed |
| **OptionsCard** | `OptionsCard.tsx` | Option chain analytics (PCR, Max Pain, IV) |
| **RrgCard** | `RrgCard.tsx` | Relative Rotation Graph visualization |
| **SectorsCard** | `SectorsCard.tsx` | Sector performance heatmap/table |
| **ScanCard** | `ScanCard.tsx` | Scan results (7 scan types) |
| **CompareCard** | `CompareCard.tsx` | Head-to-head stock comparison |
| **EarningsCard** | `EarningsCard.tsx` | Earnings calendar and analysis |
| **DividendsCard** | `DividendsCard.tsx` | Dividend data and history |
| **AnnouncementsCard** | `AnnouncementsCard.tsx` | Corporate announcements |
| **IpoCard** | `IpoCard.tsx` | IPO data and verdicts |
| **ValuationCard** | `ValuationCard.tsx` | Market valuation metrics |
| **PortfolioCard** | `PortfolioCard.tsx` | Holdings, positions, P&L |
| **TradeConfirmation** | `TradeConfirmation.tsx` | 2-phase trade confirmation UI |
| **ProgressCard** | `ProgressCard.tsx` | Generic progress indicator |
| **SuggestionCard** | `SuggestionCard.tsx` | Initial conversation suggestions |

## Supporting Components

| Component | Purpose |
|-----------|---------|
| `ChatInput.tsx` | Message input + feature buttons |
| `ChatWindow.tsx` | Main chat container |
| `FeatureBar.tsx` | 20 feature buttons row |
| `FeaturePanel.tsx` | Expanded feature panel |
| `Header.tsx` | App header |
| `Sidebar.tsx` | Conversation list |
| `MessageBubble.tsx` | Dynamic card loader |
| `MessageActions.tsx` | Copy, share, feedback on messages |
| `MarkdownRich.tsx` | Markdown renderer for AI output |
| `DataTable.tsx` | Reusable data table |
| `SkeletonCard.tsx` | Loading skeleton |
| `ThinkingScreen.tsx` | AI thinking animation |
| `TypingIndicator.tsx` | Typing dots animation |
| `TerminalLoadingScreen.tsx` | Boot animation |
| `Confetti.tsx` | Celebration animation |
| `ErrorBoundary.tsx` | Error fallback UI |
| `FeedbackModal.tsx` | Detailed feedback dialog |
| `FeedbackTagsModal.tsx` | Quick feedback tags |
| `CommandPalette.tsx` | Cmd+K command palette |
| `PWAInstallDialog.tsx` | PWA install instructions |
| `PWAProvider.tsx` | PWA context provider |
| `MobileHeader.tsx` | Mobile-specific header |
| `MobileBottomNav.tsx` | Mobile bottom navigation |
| `SuggestionChips.tsx` | Quick action chips |

## Related Notes
- [[Features]]
- [[Frontend Stack]]
- [[Architecture]]
