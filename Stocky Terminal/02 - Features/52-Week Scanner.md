---
title: 52-Week Scanner
date: 2026-04-07
tags:
  - stocky-terminal
  - scanner
  - 52-week
  - yahoo-finance
  - technical-analysis
status: published
category: features
---

# 52-Week Scanner

The 52-week scanner identifies stocks trading near their 52-week highs or lows — a key technical signal used by momentum and breakout traders.

> [!info] Why 52-Week Levels Matter
> Stocks near 52-week highs often continue higher (momentum effect), while stocks near 52-week lows may be value traps or reversal candidates. Institutional traders use these levels as filters.

## Data Source

52-week high/low data comes from Yahoo Finance's `meta` object in the quote response:

```typescript
interface ExtendedQuoteResult {
    symbol: string;
    regularMarketPrice: number;
    regularMarketChange: number;
    regularMarketChangePercent: number;
    fiftyTwoWeekHigh: number;
    fiftyTwoWeekLow: number;
    fiftyTwoWeekHighChange: number;
    fiftyTwoWeekHighChangePercent: number;
    fiftyTwoWeekLowChange: number;
    fiftyTwoWeekLowChangePercent: number;
    marketCap: number;
    averageDailyVolume3Month: number;
}
```

## Badge Logic

```typescript
function get52WBadge(price: number, high: number, low: number): string | null {
    const rangePercent = ((price - low) / (high - low)) * 100;

    if (rangePercent >= 95) return '52H'; // Within 5% of 52-week high
    if (rangePercent <= 5) return '52L';  // Within 5% of 52-week low
    return null;
}
```

| Badge | Color | Condition | Meaning |
|---|---|---|---|
| **52H** | Green | Price within 5% of 52-week high | Bullish momentum / breakout candidate |
| **52L** | Red | Price within 5% of 52-week low | Potential value or continued weakness |

## Chart Modal Integration

The chart modal displays 52-week data as part of the extended stats:

| Stat | Calculation | Display |
|---|---|---|
| 52W High | From Yahoo meta | `Rs 2,847.50` |
| 52W Low | From Yahoo meta | `Rs 1,923.15` |
| Distance from High | `(price - high) / high * 100` | `-3.2%` |
| Distance from Low | `(price - low) / low * 100` | `+41.8%` |
| Range Position | `(price - low) / (high - low) * 100` | `87.3%` (progress bar) |

The range position is displayed as a colored progress bar:
- **Green zone (70-100%)** — Near 52W high
- **Yellow zone (30-70%)** — Mid-range
- **Red zone (0-30%)** — Near 52W low

## Dashed Price Lines on Chart

When 52-week data is available, the [[TradingView Charts]] panel draws horizontal dashed lines:

- **Green dashed line** at 52-week high
- **Red dashed line** at 52-week low
- Lines extend across the full visible time range
- Labels show the price value on the Y-axis

> [!tip] Visual Context
> These lines give instant visual context: how close is the current price to major levels? This is especially useful on the 1Y timeframe where the full range is visible.

## Scanner Panel

The dedicated scanner panel shows a sortable table:

| Column | Description |
|---|---|
| Symbol | Stock ticker with click-to-chart |
| Price | Current market price |
| Change % | Day change percentage |
| 52W High | 52-week high price |
| 52W Low | 52-week low price |
| Range % | Position within 52W range |
| Badge | 52H or 52L if applicable |

Filters:
- **Near High** — Only show stocks with Range % > 90%
- **Near Low** — Only show stocks with Range % < 10%
- **All** — Show all tracked stocks with 52W data

> [!warning] Data Freshness
> 52-week high/low values from Yahoo Finance update throughout the trading day. The scanner refreshes every 15 seconds during market hours. After market close, values remain static until the next trading day.

## Related Notes

- [[TradingView Charts]]
- [[Market Data Sources]]
- [[Candlestick Pattern Detection]]
- [[Frontend Architecture]]
