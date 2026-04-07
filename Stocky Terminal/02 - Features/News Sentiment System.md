---
title: News Sentiment System
date: 2026-04-07
tags:
  - stocky-terminal
  - sentiment
  - news
  - nlp
  - rss
status: published
category: features
---

# News Sentiment System

Stocky Terminal classifies news sentiment using a keyword-based system that processes 333+ RSS feed items. Each headline receives a bullish, bearish, or neutral label displayed as colored dots in the news panel.

> [!info] Why Keywords Over AI?
> AI-based sentiment classification would require an LLM call per headline (333+ per refresh). At 15-minute intervals, that is 33,000+ LLM calls per day. Keyword classification is instant, free, and surprisingly accurate for financial headlines.

## Keyword Classifier

### Bullish Patterns (25+)

```typescript
const BULLISH_KEYWORDS = [
    'rally', 'surge', 'gains', 'recovery', 'upgrade',
    'outperform', 'bullish', 'record high', 'breakout',
    'strong buy', 'accumulate', 'overweight', 'beat estimates',
    'positive outlook', 'growth', 'expansion', 'profit rises',
    'revenue up', 'margin improvement', 'dividend increase',
    'buyback', 'stake increase', 'order win', 'contract award',
    'capacity expansion', 'market share gain',
];
```

### Bearish Patterns (25+)

```typescript
const BEARISH_KEYWORDS = [
    'drop', 'crash', 'slump', 'plunge', 'downgrade',
    'recession', 'bearish', 'selloff', 'sell-off', 'decline',
    'underperform', 'reduce', 'underweight', 'miss estimates',
    'negative outlook', 'contraction', 'profit falls',
    'revenue down', 'margin pressure', 'dividend cut',
    'debt concern', 'stake sale', 'order cancel', 'default',
    'bankruptcy', 'fraud', 'investigation', 'penalty',
];
```

## Sentiment Display

### Per-Headline Indicators

| Indicator | Color | Meaning |
|---|---|---|
| Green dot (●) | `#00ff88` | Bullish sentiment detected |
| Red dot (●) | `#ff4444` | Bearish sentiment detected |
| Gray dot (●) | `#666666` | Neutral / no keywords matched |

### Aggregate Sentiment Gauge

At the top of the news panel, an aggregate sentiment gauge shows overall market sentiment:

```
Bearish ████████░░░░░░░░░░░░ Bullish
         37% Bearish | 63% Bullish
```

The gauge is a horizontal bar divided into red (bearish) and green (bullish) segments, with percentages labeled. Only headlines from the last 2 hours contribute to the gauge.

## Classification Logic

```typescript
function classifySentiment(headline: string): 'bullish' | 'bearish' | 'neutral' {
    const lower = headline.toLowerCase();

    let bullScore = 0;
    let bearScore = 0;

    for (const keyword of BULLISH_KEYWORDS) {
        if (lower.includes(keyword)) bullScore++;
    }
    for (const keyword of BEARISH_KEYWORDS) {
        if (lower.includes(keyword)) bearScore++;
    }

    if (bullScore > bearScore) return 'bullish';
    if (bearScore > bullScore) return 'bearish';
    return 'neutral';
}
```

> [!tip] Fallback to AI Insight Direction
> When a headline is classified as neutral but mentions a tracked asset (e.g., "RELIANCE" or "TATASTEEL"), the system checks the [[AI Pipeline]] insight cache. If an AI insight exists for that asset, its direction (bullish/bearish) is used as a tiebreaker.

## Severity Scoring

Beyond sentiment, headlines are scored for severity (used by the [[Signal Generation & Aggregation]] pipeline):

| Factor | Weight | Examples |
|---|---|---|
| Source tier | 3x for T1, 2x for T2, 1.5x for T3, 1x for T4 | Reuters (T1) vs. Business Today (T4) |
| Keyword strength | 2x for strong keywords, 1x for moderate | "crash" (strong) vs. "dips" (moderate) |
| Recency | Exponential decay over 2 hours | Fresh headlines score higher |
| Asset mention | 1.5x if mentions tracked asset | "Nifty crashes 500 points" |

## Deduplication

Headlines from multiple RSS feeds often overlap. The system uses Jaccard similarity to deduplicate:

```typescript
function jaccardSimilarity(a: string, b: string): number {
    const setA = new Set(a.toLowerCase().split(/\s+/));
    const setB = new Set(b.toLowerCase().split(/\s+/));
    const intersection = new Set([...setA].filter(x => setB.has(x)));
    const union = new Set([...setA, ...setB]);
    return intersection.size / union.size;
}

// Threshold: > 0.6 similarity = duplicate
```

> [!warning] Keyword Limitations
> Keyword-based sentiment has known failure modes:
> - Negation: "Nifty does NOT crash" → classified bearish (matches "crash")
> - Sarcasm: rare in financial news but possible
> - Complex narratives: "Despite crash fears, markets rally" → matches both
>
> These edge cases are accepted tradeoffs for the speed and cost benefits.

## Related Notes

- [[News & Intelligence Sources]]
- [[Signal Generation & Aggregation]]
- [[AI Pipeline]]
- [[Data Pipeline Architecture]]
- [[Source Propaganda Flagging]]
