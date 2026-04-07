---
title: India-Specific APIs
date: 2026-04-07
tags:
  - stocky-terminal
  - india
  - nse
  - fii-dii
  - macro-dashboard
  - corporate-actions
status: published
category: apis
---

# India-Specific APIs

Stocky Terminal provides several India-specific data endpoints not found in global financial platforms. These cover institutional flows, macro indicators, corporate actions, and bulk/block deals.

> [!info] India Focus
> These endpoints are what differentiate Stocky from global alternatives like OpenBB or TradingView. Each one required custom data sourcing and processing since no single provider offers all of this data via a clean API.

## FII/DII Institutional Flows

**Endpoint:** `GET /api/data/fii-dii`

Source: NSE India (`nseindia.com/api/fiidiiTradeReact`)

```json
{
    "date": "2026-04-07",
    "fii": {
        "buyValue": 12847.32,
        "sellValue": 14231.56,
        "netValue": -1384.24
    },
    "dii": {
        "buyValue": 9423.18,
        "sellValue": 7891.45,
        "netValue": 1531.73
    },
    "unit": "crores"
}
```

See [[FII-DII Dashboard]] for the full feature documentation.

## Country Profile

**Endpoint:** `GET /api/data/country-profile?country=IN`

Provides a dossier for 30 countries, focused on their economic relationship with India:

### Countries Covered

| Region | Countries |
|---|---|
| **South Asia** | India, Pakistan, Bangladesh, Sri Lanka, Nepal |
| **East Asia** | China, Japan, South Korea, Taiwan |
| **Southeast Asia** | Singapore, Indonesia, Thailand, Vietnam, Malaysia |
| **Middle East** | UAE, Saudi Arabia, Iran, Israel |
| **Europe** | UK, Germany, France, Switzerland, Russia |
| **Americas** | USA, Canada, Brazil |
| **Africa** | South Africa, Nigeria |
| **Oceania** | Australia |

### Profile Fields

| Field | Source | Description |
|---|---|---|
| GDP | World Bank | Nominal GDP in USD |
| GDP Growth | World Bank | Annual GDP growth % |
| Population | World Bank | Latest population |
| Currency | Static | Currency name + ISO code |
| Inflation | IMF | CPI inflation rate |
| Trade with India | DGCIS | Bilateral trade volume |
| Top Exports to India | DGCIS | Top 5 export categories |
| Top Imports from India | DGCIS | Top 5 import categories |
| Political Stability | World Bank | Governance indicator |
| FDI to India | RBI | FDI inflow from this country |
| Key Companies | Static | Major companies with India presence |

## India Macro Dashboard

**Endpoint:** `GET /api/data/india-macro`

A comprehensive dashboard of India's key macroeconomic indicators:

| Indicator | Source | Frequency | Unit |
|---|---|---|---|
| **GST Collection** | PIB | Monthly | Rs Crores |
| **CPI Inflation** | MOSPI | Monthly | % |
| **IIP (Industrial Production)** | MOSPI | Monthly | Index |
| **PMI Manufacturing** | S&P Global | Monthly | Index |
| **PMI Services** | S&P Global | Monthly | Index |
| **GDP Growth** | RBI | Quarterly | % |
| **Repo Rate** | RBI | As changed | % |
| **USD/INR** | RBI | Daily | Rate |
| **FDI Inflow** | DPIIT | Quarterly | USD Billion |
| **Fiscal Deficit** | CGA | Monthly | % of GDP |
| **Forex Reserves** | RBI | Weekly | USD Billion |

### Health Score

The dashboard calculates an overall economic health score (0-100):

```typescript
function calculateHealthScore(indicators: MacroIndicators): number {
    let score = 50; // Base

    // CPI: <4% is good, >6% is bad
    if (indicators.cpi < 4) score += 10;
    else if (indicators.cpi > 6) score -= 10;

    // PMI: >50 is expansion
    if (indicators.pmiMfg > 55) score += 8;
    else if (indicators.pmiMfg < 50) score -= 8;

    // GDP: >6% is strong for India
    if (indicators.gdpGrowth > 6) score += 10;
    else if (indicators.gdpGrowth < 4) score -= 10;

    // ... similar logic for all indicators

    return Math.max(0, Math.min(100, score));
}
```

| Score Range | Label | Color |
|---|---|---|
| 80-100 | Excellent | Green |
| 60-79 | Good | Light Green |
| 40-59 | Mixed | Yellow |
| 20-39 | Concerning | Orange |
| 0-19 | Critical | Red |

## Corporate Actions

**Endpoint:** `GET /api/data/corporate-actions`

Tracks upcoming and recent corporate actions for NSE-listed companies:

| Action Type | Data | Source |
|---|---|---|
| Dividends | Ex-date, record date, amount per share | NSE |
| Stock Splits | Ratio, ex-date | NSE |
| Bonus Issues | Ratio, ex-date | NSE |
| Rights Issues | Ratio, price, record date | NSE |
| Buybacks | Open/close date, price, quantity | NSE |
| Mergers/Demergers | Effective date, terms | NSE |

## Bulk/Block Deals

**Endpoint:** `GET /api/data/bulk-deals`

| Field | Description |
|---|---|
| Symbol | Stock traded |
| Client Name | Buyer/seller name |
| Deal Type | Bulk or Block |
| Quantity | Shares traded |
| Price | Trade price |
| Date | Deal date |

> [!tip] Why Bulk Deals Matter
> Bulk and block deals reveal institutional activity that doesn't show up in regular FII/DII data. A large block deal by a known investor (e.g., Rakesh Jhunjhunwala's portfolio, LIC) can signal major institutional conviction.

> [!warning] Data Lag
> NSE publishes corporate actions and bulk/block deal data with a delay (typically end-of-day). Real-time data requires BSE/NSE paid data feeds which are cost-prohibitive for a free tool.

## Related Notes

- [[FII-DII Dashboard]]
- [[API Endpoint Reference]]
- [[Market Data Sources]]
- [[Country Dossier]]
- [[Daily Market Brief]]
