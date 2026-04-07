---
tags:
  - stocky-ai
  - engineering
  - frontend
created: 2026-04-07
status: complete
---

# Frontend Stack

## Core Technologies

| Technology | Version | Role |
|-----------|---------|------|
| **Next.js** | 16.1.6 | App Router, SSR, API routes, ISR |
| **React** | 19.2.3 | UI rendering, Server Components, automatic batching |
| **TypeScript** | 5.x | Strict mode, path aliases (`@/*`) |
| **Tailwind CSS** | 4.x | Utility-first styling via PostCSS plugin |
| **Framer Motion** | 12.36 | Spring physics animations, AnimatePresence, layoutId |
| **Radix UI** | latest | Accessible primitives (Dialog, Dropdown, Tooltip, ScrollArea) |

## PWA Configuration

> [!tip] Full Progressive Web App
> Stocky AI is installable on iOS and Android with offline fallback, cache-first static assets, and custom splash screens.

**Service Worker** (`sw.js`):
- Static assets: Cache-first (JS, CSS, images, fonts, `/_next/static/`)
- Pages/API: Network-first -> cache fallback -> `offline.html`
- Cache versioning: Build-timestamp stamped (`stocky-{timestamp}`), auto-busts on deploy

**Manifest** (`manifest.json`):
- Display: `standalone` with `window-controls-overlay` + `minimal-ui` fallback
- Shortcuts: Market Overview, Portfolio, News (direct launch)
- Icons: 192x192, 512x512, 512x512 maskable

**iOS Support**:
- `apple-mobile-web-app-capable: true` with `black-translucent` status bar
- 9 splash screen images for iPhone 13 mini through 16 Pro Max
- PWA install dialog with step-by-step share sheet instructions

## 27 Card Components

All dynamically imported via `next/dynamic` in `MessageBubble.tsx`:

| Category | Components |
|----------|-----------|
| **Analysis** | AnalysisCard, DeepResearchCard, AgentDebateCard, CouncilProgressCard, CouncilResultCard |
| **Market Data** | OverviewCard, PriceCard, NewsCard, MacroCard, FiiDiiCard, TopStocksCard |
| **Technicals** | ChartCard (TradingView embed), OptionsCard, RrgCard, SectorsCard |
| **Scanning** | ScanCard (7 scan types), CompareCard |
| **Corporate** | EarningsCard, DividendsCard, AnnouncementsCard, IpoCard, ValuationCard |
| **Portfolio** | PortfolioCard, TradeConfirmation (2-phase) |
| **Progress** | DebateProgressCard, CouncilProgressCard, ProgressCard |

## 4 Custom Hooks

| Hook | Purpose |
|------|---------|
| `useChat` | Message handling, SSE streaming, error recovery |
| `useConversations` | Conversation CRUD, list management |
| `useMediaQuery` | Responsive breakpoint detection |
| `usePWAInstall` | Install prompt detection (Android `beforeinstallprompt` + iOS UA sniffing) |

## Performance Optimizations

| Optimization | Impact |
|-------------|--------|
| Dynamic imports for cards | ~35% reduction in initial JS bundle |
| Boot screen skip (sessionStorage) | 0ms load for returning users (vs 4.2s) |
| SW cache-first for static | Instant loads for cached assets |
| Framer Motion layoutId | GPU-accelerated tab transitions |
| CSP headers | XSS attack surface hardened |
| Radix headless components | Zero CSS overhead, accessible by default |

## Key Files

| File | Purpose |
|------|---------|
| `chat/components/MessageBubble.tsx` | Dynamic card loader (27 card types) |
| `chat/components/ChatInput.tsx` | Message input with feature buttons |
| `chat/components/FeatureBar.tsx` | 20 feature buttons UI |
| `chat/components/Header.tsx` | App header with navigation |
| `chat/components/Sidebar.tsx` | Conversation list |
| `chat/components/TerminalLoadingScreen.tsx` | Boot animation |

## Related Notes
- [[Architecture]]
- [[Cards]]
- [[Features]]
- [[Tradeoffs]]
