---
title: Signal Generation & Aggregation
date: 2026-04-07
tags:
  - stocky-terminal
  - signals
  - ai
  - aggregation
  - time-weighted
  - correlation
status: published
category: ai-signals
---

# Signal Generation & Aggregation

Trade signals in Stocky Terminal are generated from high-severity news headlines every 15 minutes, then aggregated hourly using time-weighted scoring, correlation amplification, and Nifty coherence filtering.

> [!info] Signal Flow
> Headlines → AI Generation (15min) → Redis Cache → Hourly Aggregation → Validation (2h) → Display

## Signal Generation (Every 15 minutes)

### Input
The insight cron job selects high-severity headlines from the last 30 minutes:

```typescript
interface HeadlineInput {
    title: string;
    source: string;
    tier: 'T1' | 'T2' | 'T3' | 'T4';
    severity: number;  // 1-10
    detectedAssets: string[];
    sentiment: 'bullish' | 'bearish' | 'neutral';
    publishedAt: string;
}
```

Only headlines with severity >= 6 are sent to the AI for signal generation.

### AI Prompt

The prompt includes:
1. The high-severity headlines
2. Current market state (key indices, recent changes)
3. [[Ticker Context System]] for mentioned assets
4. Previous active signals (for continuity)

### Output

```typescript
interface TradeSignal {
    asset: string;           // e.g., "ONGC", "NIFTY 50", "GOLD"
    direction: 'bullish' | 'bearish';
    confidence: number;      // 0-100
    reasoning: string;       // 1-2 sentence explanation
    timeframe: string;       // "intraday", "1-3 days", "1 week"
    triggerHeadline: string;  // The headline that prompted this signal
    generatedAt: string;     // ISO timestamp
    changeReason?: string;   // If modified from previous signal
}
```

## Hourly Aggregation

The aggregation cron runs every hour and produces a consolidated signal view.

### Time-Weighted Scoring

Signals have a 12-hour lookback window with exponential time decay:

```typescript
function timeWeightedScore(signal: TradeSignal): number {
    const ageHours = (Date.now() - new Date(signal.generatedAt).getTime()) / 3_600_000;
    const decayFactor = Math.exp(-0.15 * ageHours);  // Exponential decay
    return signal.confidence * decayFactor;
}
```

| Signal Age | Decay Factor | Effective Confidence (80% base) |
|---|---|---|
| 0h (fresh) | 1.00 | 80% |
| 2h | 0.74 | 59% |
| 4h | 0.55 | 44% |
| 6h | 0.41 | 33% |
| 8h | 0.30 | 24% |
| 12h | 0.17 | 13% (near cutoff) |

### Correlation Amplification

21 asset pairs are defined with known correlations. When correlated signals align, confidence is amplified:

```typescript
const CORRELATION_PAIRS: [string, string, number][] = [
    ['CRUDE_OIL', 'ONGC', 0.8],
    ['CRUDE_OIL', 'BPCL', -0.7],      // BPCL hurt by high crude
    ['CRUDE_OIL', 'GAIL', 0.6],
    ['USD_INR', 'NIFTY_50', -0.5],     // Strong rupee = good for Nifty
    ['US_10Y', 'NIFTY_IT', -0.6],      // Rising yields = IT sell-off
    ['GOLD', 'USD_INR', 0.4],
    ['NIFTY_50', 'BANK_NIFTY', 0.9],
    ['NIFTY_50', 'NIFTY_IT', 0.7],
    ['COPPER', 'TATASTEEL', 0.6],
    ['COPPER', 'HINDALCO', 0.7],
    // ... 11 more pairs
];
```

When two correlated assets have signals in the expected direction:
- Confidence boost: `+10 * correlationFactor`
- Example: Crude Oil bullish + ONGC bullish → ONGC confidence +8

### Nifty Coherence Filtering

Individual stock signals are checked against the broad market direction:

```typescript
function checkNiftyCoherence(signal: TradeSignal, niftySignal: TradeSignal | null): boolean {
    if (!niftySignal) return true;  // No Nifty signal = no filter
    if (signal.asset === 'NIFTY 50') return true;  // Nifty itself is exempt

    // If Nifty is strongly bearish, bullish stock signals need higher confidence
    if (niftySignal.direction === 'bearish' && niftySignal.confidence > 70) {
        if (signal.direction === 'bullish' && signal.confidence < 80) {
            return false;  // Filtered out: weak bullish against strong bearish market
        }
    }
    return true;
}
```

> [!warning] Over-Filtering Risk
> Nifty coherence filtering can suppress valid contrarian signals (e.g., a defensive stock rising in a falling market). The threshold is set high (Nifty >70% confidence) to minimize false suppression.

## Previous Signal Injection

When generating new signals, previous active signals are injected into the AI prompt:

```typescript
const previousSignals = await redis.zrangebyscore('signals:active', '-inf', '+inf');
// Include in prompt:
// "Previous signals still active: ONGC bullish (75%), TATASTEEL bearish (60%)
//  If your analysis differs, include a changeReason explaining why."
```

This ensures the AI can:
1. **Maintain** signals when conditions haven't changed
2. **Upgrade/downgrade** confidence with a `changeReason`
3. **Flip direction** when fundamentals shift (with explanation)

> [!tip] changeReason Tracking
> Every signal modification includes a `changeReason` field shown to users. Example: "Upgraded from 65% to 82% after FII data showed Rs 5,200 Cr net buying in metals sector." This builds user trust in the AI system.

## Signal Display

The signals panel shows:

| Column | Description |
|---|---|
| Asset | Ticker with click-to-chart |
| Direction | Bullish (green) / Bearish (red) arrow |
| Confidence | Percentage with color gradient |
| Reasoning | 1-2 sentence explanation |
| Timeframe | Intraday / 1-3 days / 1 week |
| Age | Time since generation |
| Change | changeReason if modified |

## Related Notes

- [[AI Pipeline]]
- [[Signal Validation]]
- [[Ticker Context System]]
- [[News Sentiment System]]
- [[Data Pipeline Architecture]]
