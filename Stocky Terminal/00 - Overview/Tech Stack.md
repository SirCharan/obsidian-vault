---
title: Tech Stack
date: 2026-04-07
tags:
  - stocky-terminal
  - tech-stack
  - typescript
  - vanilla-dom
status: published
category: overview
---

# Tech Stack

Stocky Terminal is built on a deliberately minimal, zero-framework stack. Every dependency earns its place.

> [!info] Philosophy
> No React. No Vue. No Angular. No Next.js. Pure TypeScript with direct DOM manipulation. This yields a tiny bundle, instant interactions, and zero framework churn.

## Complete Technology Table

| Layer | Technology | Purpose | Notes |
|---|---|---|---|
| **Language** | TypeScript | Type-safe development | Strict mode, no `any` |
| **Bundler** | Vite | Dev server + production builds | Sub-second HMR |
| **UI Framework** | None (Vanilla DOM) | Direct DOM manipulation | Custom Panel class system |
| **Charting** | TradingView Lightweight Charts v5 | Candlestick + area charts | 35kB gzipped |
| **Pattern Detection** | technicalindicators (npm) | 13 candlestick patterns | Browser-side, zero API cost |
| **Map Engine** | deck.gl + MapLibre GL JS | 27+ layer geopolitical map | WebGL-accelerated |
| **AI / LLM** | Groq API (Llama 3.3 70B Versatile) | Trade signals, briefs, analysis | Chain-of-thought, JSON mode |
| **AI Fallback** | Ollama | Local LLM fallback | For development / outages |
| **Edge Functions** | Vercel Edge Functions | 30+ API endpoints | Global edge deployment |
| **Caching** | Upstash Redis | Server-side cache + storage | Sorted sets, TTL management |
| **Email** | Resend | Daily brief distribution | 70+ subscribers |
| **Push** | Web Push API | Real-time notifications | VAPID key authentication |
| **Market Data** | Zerodha Kite Connect | Live NSE/BSE quotes | Daily token refresh via GitHub Actions |
| **Options** | Dhan API | Options chain + Greeks | Full chain for 5 indices |
| **Quotes Fallback** | Yahoo Finance | OHLC, global indices, crypto | Cache-busting headers |
| **Crypto** | CoinGecko | 25 cryptocurrency prices | Free tier |
| **Forex** | Frankfurter + CurrencyFreaks | Exchange rates | Dual-source reliability |
| **News** | 333+ RSS Feeds | Multi-tier news pipeline | Reuters, Bloomberg, CNBC, etc. |
| **OSINT** | ACLED, USGS, NASA, GDACS, etc. | Geopolitical intelligence | 8+ sources |
| **Client Storage** | IndexedDB + localStorage | Event store + preferences | 1000 events max |
| **PWA** | Service Worker | Offline support + caching | App shell strategy |
| **Hosting** | Vercel | Edge deployment | IAD, SIN, BOM regions |
| **CI/CD** | GitHub Actions | Cron jobs + token refresh | 5 scheduled workflows |
| **SEO/AI** | llms.txt, Schema.org, ai-plugin.json | AI discoverability | 10 discovery files |

## Why Zero Frameworks

> [!tip] Performance Gains
> Without a virtual DOM diffing layer, Stocky Terminal achieves sub-50ms interaction latency. The `patchTableRows` pattern updates only changed cells, not entire component trees.

Traditional frameworks add:
- **Bundle size** — React alone is 40kB+ gzipped; Stocky's entire app shell is comparable
- **Abstraction overhead** — Virtual DOM diffing is unnecessary when you know exactly which DOM nodes change
- **Framework churn** — No migration from React 17→18→19, no hook rule gotchas, no server component complexity
- **Learning curve** — Contributors need only TypeScript and DOM APIs

The tradeoffs are real (no component ecosystem, manual state management), but for a data-dense terminal with known update patterns, vanilla TypeScript is the right call.

## Key Architectural Patterns

### Panel System
```typescript
// Base class for all UI panels
class Panel {
  element: HTMLElement;
  isLoaded: boolean;

  async init(): Promise<void>;
  render(data: unknown): void;
  destroy(): void;
}
```

### Event Bus
```typescript
// Custom event dispatch — no library needed
document.dispatchEvent(new CustomEvent('market:update', {
  detail: { symbol: 'RELIANCE', price: 2847.50 }
}));
```

### AppContext Singleton
```typescript
// Global state without Redux/Zustand
const ctx = AppContext.getInstance();
ctx.setActiveSymbol('TATASTEEL');
ctx.getMarketData(); // Returns cached data
```

## Bundle Analysis

| Chunk | Size (gzipped) | Contents |
|---|---|---|
| App shell | ~35kB | Core panels, routing, event bus |
| Charts | ~35kB | TradingView Lightweight Charts v5 |
| Map | ~120kB | deck.gl + MapLibre GL JS |
| Pattern detection | ~15kB | technicalindicators |
| Total initial load | ~85kB | App shell + charts (map lazy-loaded) |

> [!warning] Map Bundle
> The deck.gl + MapLibre combination is the largest dependency at ~120kB gzipped. It is lazy-loaded via dynamic `import()` only when the user opens the OSINT map panel.

## Related Notes

- [[Project Overview]]
- [[Frontend Architecture]]
- [[System Architecture]]
- [[Architecture Decisions]]
- [[TradingView Charts]]
- [[Map System]]
