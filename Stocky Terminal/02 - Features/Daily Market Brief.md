---
title: Daily Market Brief
date: 2026-04-07
tags:
  - stocky-terminal
  - daily-brief
  - email
  - groq
  - ai-generated
  - blog
status: published
category: features
---

# Daily Market Brief

Stocky Terminal generates and distributes automated daily market briefs at 8AM and 8PM IST, Monday through Friday. Each brief is an AI-generated comprehensive market analysis covering Indian indices, global markets, commodities, forex, and crypto.

> [!info] Distribution
> Briefs reach users through 4 channels:
> 1. **Email** — 70+ subscribers via Resend API
> 2. **Blog** — Published at terminal.stockyai.xyz/blog
> 3. **PWA Push** — Web Push notification to installed users
> 4. **In-app panel** — Brief panel within the terminal

## Data Collection

Each brief aggregates data from multiple sources:

### Market Data Inputs

| Category | Assets | Source |
|---|---|---|
| **Indian Indices** | Nifty 50, Sensex, Bank Nifty | Zerodha/Yahoo |
| **Sector Indices** | Nifty IT, Pharma, Auto, Metal, Energy, Realty, FMCG, PSU Bank | NSE/Yahoo |
| **Gift Nifty** | SGX Nifty (pre-market indication) | NSE India (with session cookies) |
| **Global Indices** | S&P 500, Nasdaq, FTSE 100, DAX, Nikkei 225, Hang Seng, Shanghai Composite, Kospi | Yahoo Finance |
| **Commodities** | Gold, Silver, Crude Oil, Natural Gas, Copper | Yahoo Finance |
| **Forex** | USD/INR, EUR/USD, GBP/USD, USD/JPY, EUR/INR | Frankfurter + CurrencyFreaks |
| **Crypto** | BTC, ETH, SOL, XRP, BNB | CoinGecko |

### AI Generation

All collected data is sent to the [[AI Pipeline]] (Groq API, Llama 3.3 70B Versatile) with a structured prompt:

```
You are a senior market analyst at an Indian financial terminal.
Generate a comprehensive market brief covering:
1. Market Overview — Key index movements and drivers
2. Sector Analysis — Which sectors led/lagged and why
3. Global Cues — Overnight US/Europe/Asia performance
4. Commodities & Forex — Major moves and implications for India
5. AI Trade Signals — 3-5 actionable signals with confidence levels
6. Outlook — What to watch in the next session

Use specific numbers. Be concise but insightful. Format as HTML.
```

> [!tip] Chain-of-Thought
> The prompt uses chain-of-thought reasoning: the model first analyzes each data category, then synthesizes a coherent narrative. This produces more insightful briefs than simply summarizing each number.

## Storage & Distribution

### Redis Storage

Briefs are stored as HTML in a Redis sorted set:

```typescript
// Edition numbering
const currentEdition = await redis.get('blog:edition');
const newEdition = (parseInt(currentEdition || '0', 10)) + 1;
await redis.set('blog:edition', newEdition.toString());

// Store brief
await redis.zadd('blog:posts', {
    score: newEdition,
    member: JSON.stringify({
        edition: newEdition,
        type: briefType,  // 'morning' | 'evening'
        html: generatedHTML,
        date: new Date().toISOString(),
        subject: `Stocky Brief #${newEdition} — ${briefType === 'morning' ? 'Morning' : 'Evening'}`,
    })
});
```

### Email Distribution

```typescript
// Send to all subscribers via Resend
const subscribers = await redis.smembers('subscribers');
for (const email of subscribers) {
    await resend.emails.send({
        from: 'Stocky Terminal <brief@stockyai.xyz>',
        to: email,
        subject: `Stocky Brief #${edition} — ${type}`,
        html: personalizedHTML,
    });
    // Rate limit: 2 emails/second
    await new Promise(r => setTimeout(r, 500));
}
```

> [!warning] Rate Limiting
> Resend allows 2 emails/second on the current plan. With 70+ subscribers, a full send takes ~35 seconds. If the subscriber list grows to 500+, batch sending with higher-tier Resend plans will be needed.

## Rating System

Each subscriber can rate a brief 1-10:

| Rating | Label | Color |
|---|---|---|
| 1-3 | Poor | Red |
| 4-6 | Average | Yellow |
| 7-8 | Good | Green |
| 9-10 | Excellent | Gold |

Ratings are stored per-subscriber, per-edition with a 90-day TTL in Redis. The average rating is displayed on the blog page for each brief.

## PDF Download

Users can download any brief as a PDF:

1. Client requests brief HTML from `/api/blog/post?edition=N`
2. Browser-side PDF generation using `html2pdf.js` (lazy-loaded)
3. Styled with print-friendly CSS (no dark theme, proper margins)

## Blog

The blog at `terminal.stockyai.xyz/blog` serves as a public archive:
- All briefs are listed in reverse chronological order
- Each brief has its own shareable URL
- Social sharing buttons for WhatsApp, Telegram, LinkedIn, X
- RSS feed for the blog itself

## Brief Schedule

```mermaid
timeline
    title Daily Brief Schedule (IST)
    8:00 AM : Morning Brief
              Data collection starts
    8:02 AM : AI generation complete
              Redis storage
    8:03 AM : Email distribution begins
              (~35s for 70 subscribers)
    8:04 AM : Push notifications sent
              Blog post published
    8:00 PM : Evening Brief
              Same pipeline as morning
```

## Related Notes

- [[AI Pipeline]]
- [[Email System]]
- [[Database & Caching]]
- [[Data Pipeline Architecture]]
- [[Technical Learnings]]
- [[PWA & Push Notifications]]
