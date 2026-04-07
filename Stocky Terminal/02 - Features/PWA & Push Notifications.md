---
title: PWA & Push Notifications
date: 2026-04-07
tags:
  - stocky-terminal
  - pwa
  - service-worker
  - push-notifications
  - web-push
status: published
category: features
---

# PWA & Push Notifications

Stocky Terminal is a Progressive Web App with full offline support and Web Push notifications for real-time alerts.

> [!info] Install as App
> Users can install Stocky Terminal as a standalone app on desktop (Chrome, Edge) and mobile (Android, iOS 16.4+). The PWA behaves like a native app with its own window and icon.

## Service Worker

### Caching Strategy

The service worker uses an **app shell** caching strategy:

| Resource Type | Strategy | Cache Name |
|---|---|---|
| HTML (app shell) | Cache First, Network Fallback | `stocky-shell-v2` |
| CSS, JS bundles | Cache First (versioned) | `stocky-assets-v2` |
| Map tiles | Cache First, Network Fallback | `stocky-tiles-v1` |
| API responses | Network First, Cache Fallback | `stocky-data-v1` |
| Fonts | Cache First | `stocky-fonts-v1` |
| Images | Cache First | `stocky-images-v1` |

```typescript
// Service worker fetch handler
self.addEventListener('fetch', (event: FetchEvent) => {
    const url = new URL(event.request.url);

    if (url.pathname.startsWith('/api/')) {
        // Network first for API calls
        event.respondWith(networkFirst(event.request, 'stocky-data-v1'));
    } else if (url.pathname.match(/\.(js|css)$/)) {
        // Cache first for versioned assets
        event.respondWith(cacheFirst(event.request, 'stocky-assets-v2'));
    } else {
        // Cache first for app shell
        event.respondWith(cacheFirst(event.request, 'stocky-shell-v2'));
    }
});
```

### Offline Indicator

When the browser goes offline, a banner appears at the top:

```
⚠ You are offline. Showing cached data. Prices may be stale.
```

The banner auto-hides when connectivity returns, and a brief "Back online" toast confirms reconnection.

> [!warning] Stale Bundle Issue
> Service workers can serve stale JavaScript bundles after a deployment. Stocky handles this by including a build hash in the service worker filename and using `skipWaiting()` + `clients.claim()` to activate new versions immediately. See [[Technical Learnings]] for the full solution.

## Web Push Notifications

### VAPID Authentication

Web Push uses VAPID (Voluntary Application Server Identification) keys:

```typescript
// Client: Subscribe to push
const registration = await navigator.serviceWorker.ready;
const subscription = await registration.pushManager.subscribe({
    userVisibleOnly: true,
    applicationServerKey: urlBase64ToUint8Array(VAPID_PUBLIC_KEY),
});

// Send subscription to server
await fetch('/api/push/subscribe', {
    method: 'POST',
    body: JSON.stringify(subscription),
});
```

### Push Triggers

| Event | Priority | Message |
|---|---|---|
| Daily morning brief | Normal | "Good morning! Your market brief is ready" |
| Daily evening brief | Normal | "Your evening market recap is ready" |
| High-confidence trade signal | High | "New signal: RELIANCE — Bullish (85% confidence)" |
| Market crash alert | Urgent | "Market Alert: Nifty down 3%+" |
| 52W high breakout | Normal | "TATASTEEL hit a new 52-week high" |

### Smart Install Prompt

The PWA install prompt is deferred and shown contextually:

```typescript
let deferredPrompt: BeforeInstallPromptEvent | null = null;

window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault();
    deferredPrompt = e;
    // Show install button only after user has used the app for 2+ minutes
    setTimeout(() => showInstallButton(), 120_000);
});
```

> [!tip] Install Rate
> Deferring the install prompt until after 2 minutes of engagement increases install acceptance rates significantly compared to showing it immediately on load.

## Manifest

```json
{
    "name": "Stocky Terminal",
    "short_name": "Stocky",
    "description": "Open-source Bloomberg alternative for India",
    "start_url": "/",
    "display": "standalone",
    "background_color": "#0a0a0f",
    "theme_color": "#00ff88",
    "icons": [
        { "src": "/icon-192.png", "sizes": "192x192", "type": "image/png" },
        { "src": "/icon-512.png", "sizes": "512x512", "type": "image/png" }
    ]
}
```

## Related Notes

- [[Frontend Architecture]]
- [[Deployment]]
- [[Daily Market Brief]]
- [[Technical Learnings]]
- [[Signal Generation & Aggregation]]
