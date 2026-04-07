---
title: Source Propaganda Flagging
date: 2026-04-07
tags:
  - stocky-terminal
  - propaganda
  - state-media
  - osint
  - media-bias
status: published
category: osint-map
---

# Source Propaganda Flagging

Stocky Terminal identifies and flags 10 state-controlled media outlets in the news feed. Flagged sources display an orange "State Media" badge, alerting users to potential propaganda or state-directed narrative.

> [!info] Not Censorship
> State media articles are NOT removed or hidden. They appear in the normal news feed with an orange badge. The goal is informed consumption, not censorship. State media often breaks news about their own government's actions before independent outlets.

## Flagged Sources

| Source | Country | Government Control | RSS Feeds |
|---|---|---|---|
| **TASS** | Russia | Federal state news agency | 1 |
| **RT (Russia Today)** | Russia | Government-funded broadcaster | 2 |
| **Sputnik** | Russia | Government-owned media | 1 |
| **Xinhua** | China | Official state press agency | 2 |
| **CGTN** | China | State-run television network | 1 |
| **Global Times** | China | CCP-affiliated tabloid | 1 |
| **IRNA** | Iran | State news agency | 1 |
| **Press TV** | Iran | State-run English news | 1 |
| **TRT World** | Turkey | State broadcaster | 1 |
| **Al Mayadeen** | Lebanon | Hezbollah-affiliated | 1 |

## Implementation

```typescript
const STATE_MEDIA_DOMAINS = [
    'tass.com',
    'rt.com',
    'sputniknews.com',
    'sputnikglobe.com',
    'xinhuanet.com',
    'xinhua.net',
    'cgtn.com',
    'globaltimes.cn',
    'irna.ir',
    'presstv.ir',
    'presstv.com',
    'trtworld.com',
    'almayadeen.net',
];

function isStateMedia(sourceUrl: string): boolean {
    const hostname = new URL(sourceUrl).hostname.toLowerCase();
    return STATE_MEDIA_DOMAINS.some(domain =>
        hostname === domain || hostname.endsWith('.' + domain)
    );
}
```

> [!tip] Case-Insensitive Matching
> Domain matching is case-insensitive and checks both exact domain and subdomains (e.g., `english.cgtn.com` matches `cgtn.com`). This prevents bypass via subdomain variations.

## Badge Display

In the news panel, flagged sources show:

```
[State Media] TASS — Russia deploys new missile defense system
```

The badge is:
- **Color:** Orange (`#ff8c00`)
- **Position:** Before the source name
- **Tooltip:** "This source is a state-controlled media outlet. Content may reflect government narrative."

## Why These 10?

Selection criteria:
1. **Direct government ownership or control** — Not just bias, but structural control
2. **English-language RSS feeds available** — Must be in Stocky's feed pipeline
3. **Market-relevant content** — Must publish financial/geopolitical news
4. **Documented propaganda history** — Multiple press freedom organizations flag them

Sources NOT flagged (but considered):
- **Al Jazeera** — Qatari government funded but editorially independent on non-Qatar topics
- **BBC** — UK government funded but editorially independent (Royal Charter)
- **NHK** — Japanese public broadcaster with editorial independence
- **WION** — Indian, private ownership

> [!warning] Bias vs. Propaganda
> This system flags state CONTROL, not editorial bias. All news sources have bias. The distinction is whether the government can dictate editorial content. Only sources where the government has structural control over editorial decisions are flagged.

## Impact on Sentiment Scoring

State media articles receive no special treatment in sentiment scoring — they are classified by the same keyword system as all other sources. However, they are Tier 4 (lowest weight), meaning their severity scores are naturally lower.

The [[Signal Generation & Aggregation]] pipeline does not use state media headlines as trigger events for signal generation. They contribute to the overall news feed but don't drive AI analysis.

## Related Notes

- [[News & Intelligence Sources]]
- [[News Sentiment System]]
- [[OSINT Data Sources]]
- [[Map System]]
