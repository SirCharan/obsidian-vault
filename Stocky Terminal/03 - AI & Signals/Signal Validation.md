---
title: Signal Validation
date: 2026-04-07
tags:
  - stocky-terminal
  - signals
  - validation
  - live-price
  - accuracy
status: published
category: ai-signals
---

# Signal Validation

Every 2 hours, a cron job validates all active trade signals against live market prices. Signals that contradict market reality are either removed or flipped.

> [!info] Purpose
> AI-generated signals can become stale or wrong as new information arrives. Validation ensures users never see a "bullish ONGC" signal while ONGC is actually crashing. This builds trust in the signal system.

## Validation Logic

```mermaid
flowchart TB
    START["Fetch all active signals<br/>from Redis"] --> LOOP["For each signal"]
    LOOP --> PRICE["Fetch live price<br/>from Yahoo Finance"]
    PRICE --> CALC["Calculate price change<br/>since signal generation"]
    CALC --> CHECKCheck contradiction

    CHECK -->|"No contradiction<br/>(price aligns)"| KEEP["Keep signal<br/>as-is"]
    CHECK -->|">0.5% contradiction"| REMOVE["Remove signal<br/>from Redis"]
    CHECK -->|">1.5% strong<br/>contradiction"| FLIP["Flip direction<br/>Confidence -15"]

    KEEP --> NEXT["Next signal"]
    REMOVE --> NEXT
    FLIP --> NEXT
```

## Contradiction Detection

```typescript
interface ValidationResult {
    signal: TradeSignal;
    currentPrice: number;
    priceAtGeneration: number;
    priceChangePercent: number;
    contradicts: boolean;
    severity: 'none' | 'mild' | 'strong';
}

function validateSignal(signal: TradeSignal, currentPrice: number, priceAtGeneration: number): ValidationResult {
    const changePercent = ((currentPrice - priceAtGeneration) / priceAtGeneration) * 100;

    let contradicts = false;
    let severity: 'none' | 'mild' | 'strong' = 'none';

    if (signal.direction === 'bullish' && changePercent < -0.5) {
        contradicts = true;
        severity = changePercent < -1.5 ? 'strong' : 'mild';
    }
    if (signal.direction === 'bearish' && changePercent > 0.5) {
        contradicts = true;
        severity = changePercent > 1.5 ? 'strong' : 'mild';
    }

    return { signal, currentPrice, priceAtGeneration, priceChangePercent: changePercent, contradicts, severity };
}
```

## Thresholds

| Condition | Action | Example |
|---|---|---|
| Price aligns with signal | No change | Bullish signal, price up 0.8% |
| >0.5% mild contradiction | **Remove signal** | Bullish signal, price down 0.7% |
| >1.5% strong contradiction | **Flip direction, confidence -15** | Bullish signal, price down 2.3% → Bearish at (confidence - 15)% |
| Direction already flipped once | Remove (don't double-flip) | Prevents oscillation |

## Flip Behavior

When a signal is strongly contradicted:

```typescript
if (severity === 'strong' && !signal.previouslyFlipped) {
    signal.direction = signal.direction === 'bullish' ? 'bearish' : 'bullish';
    signal.confidence = Math.max(signal.confidence - 15, 30);  // Floor at 30%
    signal.changeReason = `Direction flipped: ${signal.asset} moved ${Math.abs(changePercent).toFixed(1)}% against original ${originalDirection} signal`;
    signal.previouslyFlipped = true;
    // Preserve original updatedAt
}
```

> [!warning] Preserving updatedAt
> The `updatedAt` timestamp is intentionally NOT updated during validation. This preserves the signal's apparent age for time-weighted scoring in the [[Signal Generation & Aggregation]] pipeline. Updating it would artificially boost a flipped signal's weight.

> [!tip] Why Not Just Remove All Contradicted Signals?
> Strong contradictions often indicate a genuine trend reversal. Flipping the signal captures this reversal information rather than leaving a gap. The confidence reduction (-15) appropriately reflects uncertainty about the new direction.

## Validation Frequency

| Time | Reason |
|---|---|
| Every 2 hours | Balance between freshness and API load |
| Not during market close | 6:30 PM - 9:00 AM IST: prices don't change |
| Skipped on weekends | No market data to validate against |

## Edge Cases

1. **Signal for asset with no live price** (e.g., market closed) → Skip validation, keep signal
2. **Signal for commodity/forex** (24h market) → Validate even outside Indian market hours
3. **Signal generated <30 minutes ago** → Skip (too early to validate)
4. **Multiple signals for same asset** → Validate each independently

## Metrics

The validation cron logs:

| Metric | Purpose |
|---|---|
| Signals validated | Total checked |
| Signals kept | No contradiction |
| Signals removed | Mild contradiction |
| Signals flipped | Strong contradiction |
| Average age of removed signals | Quality indicator |
| Validation latency | Performance monitoring |

## Related Notes

- [[Signal Generation & Aggregation]]
- [[AI Pipeline]]
- [[Data Pipeline Architecture]]
- [[Technical Learnings]]
- [[Code Audit Fixes]]
