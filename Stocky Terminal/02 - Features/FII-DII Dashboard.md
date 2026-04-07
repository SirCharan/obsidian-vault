---
title: FII-DII Dashboard
date: 2026-04-07
tags:
  - stocky-terminal
  - fii-dii
  - institutional-flow
  - nse-india
  - india-market
status: published
category: features
---

# FII-DII Dashboard

The FII/DII (Foreign Institutional Investors / Domestic Institutional Investors) dashboard shows real-time institutional trading flows — the single most watched data point by Indian market participants.

> [!info] Why FII/DII Matters
> FII flows drive 60-70% of Indian market direction on any given day. When FIIs are net buyers, Nifty tends to rise. When they sell aggressively, markets fall. DII buying often provides a floor. Tracking these flows is essential for Indian market analysis.

## Data Source

Data comes directly from NSE India's internal API:

```
GET https://www.nseindia.com/api/fiidiiTradeReact
```

> [!warning] Session Cookie Required
> NSE India blocks direct API calls without a valid session cookie. The endpoint requires a two-step process:
> 1. Hit `https://www.nseindia.com` to get a session cookie
> 2. Use that cookie in the API request headers
>
> See [[Technical Learnings]] for the full session cookie pattern.

## Data Structure

The API returns daily buy/sell values for each category:

| Field | Type | Example |
|---|---|---|
| FII/FPI Buy Value | Number (Crores) | `12,847.32` |
| FII/FPI Sell Value | Number (Crores) | `14,231.56` |
| FII/FPI Net Value | Number (Crores) | `-1,384.24` |
| DII Buy Value | Number (Crores) | `9,423.18` |
| DII Sell Value | Number (Crores) | `7,891.45` |
| DII Net Value | Number (Crores) | `+1,531.73` |

## Visual Display

### Bar Chart

The dashboard renders a horizontal bar chart showing:
- **Green bars** for buy values
- **Red bars** for sell values
- **Net value** displayed as a badge (green if positive, red if negative)

```
FII/FPI
Buy   ████████████████████ Rs 12,847 Cr
Sell  ██████████████████████ Rs 14,232 Cr
Net   [-1,384 Cr]  🔴

DII
Buy   ████████████████ Rs 9,423 Cr
Sell  █████████████ Rs 7,891 Cr
Net   [+1,532 Cr]  🟢
```

### Summary Card

At the top of the dashboard:

| Metric | Display |
|---|---|
| **FII Net** | Large font, color-coded |
| **DII Net** | Large font, color-coded |
| **Combined Net** | Sum of FII + DII net |
| **Trend** | 5-day direction arrow |

## Auto-Loading

The FII/DII panel automatically fetches data on initialization:

```typescript
class FIIDIIPanel extends Panel {
    async init(): Promise<void> {
        this.isLoaded = true;
        await this.refresh();
        // Auto-refresh every 5 minutes during market hours
        this.timer = setInterval(() => this.refresh(), 300_000);
    }

    async refresh(): Promise<void> {
        const data = await fetch('/api/data/fii-dii').then(r => r.json());
        this.render(data);
    }
}
```

> [!tip] Market Hours Only
> FII/DII data updates once per day after market close (~6 PM IST). During market hours, provisional data may be available. The panel shows a "Provisional" badge when data might not be final.

## Correlation with Market Movement

The daily brief (see [[Daily Market Brief]]) includes FII/DII data in its AI analysis. The Groq model considers institutional flows when generating the market outlook:

- **FII net positive + DII net positive** → Strong bullish signal
- **FII net negative + DII net positive** → Mixed, often range-bound
- **FII net negative + DII net negative** → Bearish signal (rare)
- **FII net positive + DII net negative** → Rally led by foreign money

## Related Notes

- [[India-Specific APIs]]
- [[Daily Market Brief]]
- [[Market Data Sources]]
- [[News Sentiment System]]
- [[Technical Learnings]]
