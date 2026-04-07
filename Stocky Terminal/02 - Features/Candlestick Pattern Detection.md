---
title: Candlestick Pattern Detection
date: 2026-04-07
tags:
  - stocky-terminal
  - candlestick
  - technical-analysis
  - pattern-detection
  - technicalindicators
status: published
category: features
---

# Candlestick Pattern Detection

Stocky Terminal detects 13 candlestick patterns entirely browser-side using the `technicalindicators` npm package. Zero API calls, zero server cost — pattern detection runs in the client's browser on OHLC data already fetched for charting.

> [!info] Zero API Cost
> Unlike services that charge per-pattern-scan, all detection happens in ~10ms on the client using the `technicalindicators` library (~15kB gzipped). The OHLC data is reused from the chart — no additional data fetch needed.

## Supported Patterns

### Bullish Patterns

| Pattern | Candles | Signal Strength | Description |
|---|---|---|---|
| **Bullish Engulfing** | 2 | Strong | Large green candle completely engulfs prior red candle |
| **Bullish Harami** | 2 | Moderate | Small green candle within prior large red candle's body |
| **Morning Star** | 3 | Strong | Red → small body → green; classic reversal |
| **Hammer** | 1 | Moderate | Small body, long lower shadow (2x+ body), little upper shadow |
| **Piercing Line** | 2 | Moderate | Green candle opens below prior close, closes above midpoint |
| **Three White Soldiers** | 3 | Strong | Three consecutive green candles with higher closes |
| **Doji** | 1 | Weak | Open ≈ Close; indecision, potential reversal |

### Bearish Patterns

| Pattern | Candles | Signal Strength | Description |
|---|---|---|---|
| **Bearish Engulfing** | 2 | Strong | Large red candle engulfs prior green candle |
| **Bearish Harami** | 2 | Moderate | Small red candle within prior large green candle's body |
| **Evening Star** | 3 | Strong | Green → small body → red; bearish reversal |
| **Hanging Man** | 1 | Moderate | Same shape as hammer but at top of uptrend |
| **Dark Cloud Cover** | 2 | Moderate | Red candle opens above prior high, closes below midpoint |
| **Three Black Crows** | 3 | Strong | Three consecutive red candles with lower closes |

## Implementation

```typescript
import {
    bullishengulfingpattern,
    bearishengulfingpattern,
    morningstar,
    eveningstar,
    hammerpattern,
    hangingman,
    doji,
    threewhitesoldiers,
    threeblackcrows,
    piercingline,
    darkcloudcover,
    bullishharami,
    bearishharami,
} from 'technicalindicators';

interface PatternResult {
    name: string;
    type: 'bullish' | 'bearish' | 'neutral';
    index: number;      // Position in OHLC array where pattern ends
    strength: 'strong' | 'moderate' | 'weak';
}

function detectPatterns(ohlc: OHLC[]): PatternResult[] {
    const input = {
        open: ohlc.map(c => c.open),
        high: ohlc.map(c => c.high),
        low: ohlc.map(c => c.low),
        close: ohlc.map(c => c.close),
    };

    const results: PatternResult[] = [];

    // Each function returns boolean[] — true at indices where pattern detected
    const bullishEngulfing = bullishengulfingpattern(input);
    bullishEngulfing.forEach((detected, i) => {
        if (detected) results.push({
            name: 'Bullish Engulfing', type: 'bullish', index: i, strength: 'strong'
        });
    });

    // ... repeat for all 13 patterns
    return results;
}
```

## Display

Detected patterns appear as colored badges below the TradingView chart:

- **Green badges** for bullish patterns (e.g., "Morning Star", "Bullish Engulfing")
- **Red badges** for bearish patterns (e.g., "Evening Star", "Three Black Crows")
- **Gray badges** for neutral patterns (e.g., "Doji")

Each badge is clickable: clicking scrolls the chart to center on the candles where the pattern was detected and highlights them with a vertical band.

> [!tip] Pattern Recency
> Only patterns detected in the last 5 trading days are shown as badges by default. Older patterns are available via a "Show All" toggle. This keeps the display focused on actionable patterns.

## Performance

| Metric | Value |
|---|---|
| Detection time (250 bars) | <10ms |
| Detection time (1000 bars) | ~30ms |
| Library size | ~15kB gzipped |
| API cost | $0 (browser-side) |
| Data cost | $0 (reuses chart OHLC) |

> [!warning] False Positives
> Candlestick patterns in isolation have limited predictive power. Stocky uses them as one input alongside AI signals, sentiment, and institutional flow data. The patterns should be viewed as visual cues, not trade recommendations.

## Related Notes

- [[TradingView Charts]]
- [[Signal Generation & Aggregation]]
- [[News Sentiment System]]
- [[Tech Stack]]
