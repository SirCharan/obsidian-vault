---
title: Options Chain
date: 2026-04-07
tags:
  - stocky-terminal
  - options
  - dhan-api
  - greeks
  - derivatives
status: published
category: features
---

# Options Chain

Stocky Terminal provides a full options chain with Greeks for India's major index options, powered by the Dhan API.

> [!info] Supported Indices
> - **Nifty 50** — Most liquid index options globally
> - **Bank Nifty** — Banking sector index
> - **Sensex** — BSE 30-stock index
> - **FINNifty** — Financial services index
> - **MIDCPNifty** — Midcap index

## Data Source

The Dhan API provides comprehensive options chain data:

```
GET /api/market/options?index=NIFTY
```

### Response Fields

| Field | Type | Description |
|---|---|---|
| `strikePrice` | number | Option strike price |
| `expiryDate` | string | Expiry date (weekly/monthly) |
| `callOI` | number | Call open interest |
| `putOI` | number | Put open interest |
| `callIV` | number | Call implied volatility |
| `putIV` | number | Put implied volatility |
| `callDelta` | number | Call delta |
| `callGamma` | number | Call gamma |
| `callTheta` | number | Call theta |
| `callVega` | number | Call vega |
| `putDelta` | number | Put delta |
| `putGamma` | number | Put gamma |
| `putTheta` | number | Put theta |
| `putVega` | number | Put vega |
| `callLTP` | number | Call last traded price |
| `putLTP` | number | Put last traded price |
| `callChange` | number | Call price change |
| `putChange` | number | Put price change |

## Key Metrics

### Displayed at Top

| Metric | Calculation | Significance |
|---|---|---|
| **ATM Strike** | Nearest strike to spot price | Current "at the money" level |
| **PCR (Put/Call Ratio)** | Total Put OI / Total Call OI | >1 = bearish sentiment, <1 = bullish |
| **Max Pain** | Strike where total options premium paid is maximized | Theoretical price magnet at expiry |
| **IV (Implied Volatility)** | ATM options average IV | Market's expected move |

### Greeks Explained

| Greek | Measures | Range | Use |
|---|---|---|---|
| **Delta (Δ)** | Price sensitivity to underlying | 0 to ±1 | Position sizing, hedge ratio |
| **Gamma (Γ)** | Rate of delta change | 0 to ~0.05 | Risk of delta shift |
| **Theta (Θ)** | Time decay per day | Negative for long | Cost of holding |
| **Vega (ν)** | Sensitivity to IV change | 0 to ~20 | Volatility exposure |

## Display Layout

The options chain displays ±10 strikes around ATM:

```
Calls                    Strike    Puts
LTP  Change  OI  IV  Δ  | 24,500 |  Δ  IV  OI  Change  LTP
LTP  Change  OI  IV  Δ  | 24,550 |  Δ  IV  OI  Change  LTP
LTP  Change  OI  IV  Δ  | 24,600 |  Δ  IV  OI  Change  LTP
                         ─── ATM ───
LTP  Change  OI  IV  Δ  | 24,650 |  Δ  IV  OI  Change  LTP
LTP  Change  OI  IV  Δ  | 24,700 |  Δ  IV  OI  Change  LTP
```

- **ATM strike** is highlighted with a distinct background color
- **ITM (In The Money)** strikes have a subtle background tint
- **OTM (Out of The Money)** strikes have a standard background
- **OI change** is color-coded: green for OI buildup, red for OI unwinding

## Refresh Rates

| Layer | Interval | TTL |
|---|---|---|
| Client polling | 30 seconds | — |
| Vercel edge cache | — | 10 seconds |
| Redis cache | — | 30 seconds |
| Dhan API rate limit | — | Generous for index options |

> [!tip] Max Pain Calculation
> Max pain is calculated by summing the total intrinsic value of all in-the-money calls and puts at each strike. The strike where this total is maximum is the max pain strike — where option writers profit most and option buyers lose most.

> [!warning] Expiry Selection
> The options chain defaults to the nearest weekly expiry. Monthly expiry is available via a dropdown. Weekly expiry options (introduced for Nifty and Bank Nifty) have much higher OI and are more relevant for short-term trading.

## Related Notes

- [[Market Data Sources]]
- [[India-Specific APIs]]
- [[API Layer Design]]
- [[Signal Generation & Aggregation]]
