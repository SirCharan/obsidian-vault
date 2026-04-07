---
title: Technical Learnings
date: 2026-04-07
tags:
  - stocky-terminal
  - learnings
  - debugging
  - gotchas
  - production-issues
status: published
category: decisions
---

# Technical Learnings

Hard-won technical lessons from building and operating Stocky Terminal in production. Each learning represents a bug, unexpected behavior, or non-obvious solution discovered during development.

> [!info] Format
> Each learning includes: **Problem** (what went wrong), **Root Cause** (why), **Fix** (how it was solved), **Lesson** (what to remember).

## 1. Gift Nifty Session Cookies

**Problem:** Gift Nifty API calls to NSE India started returning 403 Forbidden after working fine during development.

**Root Cause:** NSE India requires a valid session cookie obtained by first visiting the homepage. The session cookie expires after ~15 minutes. During development, the browser had a valid cookie from manual browsing; in production (Vercel Edge), there was no cookie.

**Fix:**
```typescript
// Two-step request pattern
async function fetchGiftNifty(): Promise<GiftNiftyData> {
    // Step 1: Get session cookie
    const session = await fetch('https://www.nseindia.com', {
        headers: { 'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)...' }
    });
    const cookies = session.headers.get('set-cookie') || '';

    // Step 2: Use cookie for API call
    const data = await fetch('https://www.nseindia.com/api/liveEquity/...', {
        headers: {
            'Cookie': cookies,
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)...',
        }
    });
    return data.json();
}
```

**Lesson:** Always test API integrations from the same environment as production (edge function, not browser). Session-based APIs need explicit cookie management.

## 2. Yahoo Finance Cache-Busting

**Problem:** Yahoo Finance API intermittently returned stale data (previous day's close during market hours).

**Root Cause:** Yahoo's CDN aggressively caches responses. The same URL returns cached data across multiple edge nodes.

**Fix:** Add a timestamp cache-buster parameter:
```typescript
const url = `https://query1.finance.yahoo.com/v8/finance/chart/${symbol}?range=1d&_=${Date.now()}`;
```

**Lesson:** Free APIs often have aggressive CDN caching. Always test data freshness, not just data correctness.

## 3. Edition Numbering Race Condition

**Problem:** Two consecutive briefs (morning at 8:00 AM, manual retry at 8:05 AM) received the same edition number.

**Root Cause:** The edition number used a read-then-set pattern:
```typescript
// BUG: Non-atomic read-then-set
const current = await redis.get('blog:edition');
const next = parseInt(current, 10) + 1;
await redis.set('blog:edition', next.toString());
```
If two cron executions overlap, both read the same value.

**Fix:** Use Redis `INCR` for atomic increment:
```typescript
// FIX: Atomic increment
const next = await redis.incr('blog:edition');
```

**Lesson:** Any read-then-write pattern on shared state is a race condition. Use atomic operations (INCR, SETNX, Lua scripts) in Redis.

> [!warning] Duplicate Briefs
> The duplicate edition resulted in two emails with the same edition number being sent to all subscribers. A guard was added to check if an edition already exists before sending.

## 4. Signal Flip Fix

**Problem:** A signal would flip from bullish to bearish, then back to bullish on the next validation cycle — oscillating indefinitely.

**Root Cause:** The validation logic would flip a strongly contradicted signal, but the flipped signal would then be validated against a price that had partially recovered, causing another flip.

**Fix:** Added a `previouslyFlipped` flag — signals can only be flipped once. If a flipped signal is still contradicted, it is removed rather than flipped again.

**Lesson:** State machines need termination conditions. Any bidirectional transition (bullish ↔ bearish) risks oscillation without a "flipped once" guard.

## 5. ONGC Ticker Context Fix

**Problem:** AI generated bullish signals for ONGC when crude oil prices were falling. ONGC is an upstream oil producer — falling crude is bearish for ONGC.

**Root Cause:** The LLM's general knowledge conflated upstream (ONGC, oil producer — benefits from high crude) with downstream (BPCL, oil refiner — benefits from low crude). Without explicit context, the model made incorrect sector assumptions.

**Fix:** Created the [[Ticker Context System]] with explicit `benefitsFrom` and `hurtsFrom` arrays for 15 major assets. Injected into all AI prompts.

**Lesson:** LLMs have general but imprecise domain knowledge. For specialized domains (Indian energy sector), explicit context injection dramatically improves accuracy.

## 6. Service Worker Stale Bundles

**Problem:** After deploying a new version, some users reported seeing the old UI with broken API calls (old endpoints hitting new backend).

**Root Cause:** The Service Worker was caching JavaScript bundles with a "cache first" strategy. New deployments changed the bundle content but not the URL pattern, so the SW served stale bundles.

**Fix:**
1. Include build hash in service worker filename: `sw-${BUILD_HASH}.js`
2. Use `skipWaiting()` + `clients.claim()` for immediate activation
3. Clean old caches on activation:
```typescript
self.addEventListener('activate', (event) => {
    event.waitUntil(
        caches.keys().then(keys =>
            Promise.all(keys
                .filter(key => key !== CURRENT_CACHE_VERSION)
                .map(key => caches.delete(key))
            )
        )
    );
    self.clients.claim();
});
```

**Lesson:** Service Worker cache invalidation is one of the two hard problems in computer science. Use versioned cache names and aggressive cleanup.

## 7. Stale Weekend Data Detection

**Problem:** On Saturday/Sunday, the terminal displayed Friday's closing prices without any indication that data was stale.

**Root Cause:** No staleness detection — the UI rendered whatever the API returned, and the API returned cached Friday data.

**Fix:** Added a staleness check:
```typescript
function isDataStale(lastUpdated: string): boolean {
    const age = Date.now() - new Date(lastUpdated).getTime();
    const EIGHTEEN_HOURS = 18 * 60 * 60 * 1000;
    return age > EIGHTEEN_HOURS;
}
// If stale, show "Markets Closed" banner
```

**Lesson:** Real-time displays must explicitly handle non-real-time states (weekends, holidays, market hours). Never assume data is fresh just because it exists.

> [!tip] Holiday Calendar
> A future improvement: maintain an Indian market holiday calendar (NSE publishes these annually) and show "Market Holiday — [Holiday Name]" instead of generic "Markets Closed."

## Related Notes

- [[Code Audit Fixes]]
- [[Architecture Decisions]]
- [[Database & Caching]]
- [[Signal Validation]]
- [[Ticker Context System]]
- [[PWA & Push Notifications]]
