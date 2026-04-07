---
title: SEO & AI Discoverability
date: 2026-04-07
tags:
  - stocky-terminal
  - seo
  - ai-discoverability
  - llms-txt
  - schema-org
  - robots
status: published
category: devops
---

# SEO & AI Discoverability

Stocky Terminal implements 10 discovery files to ensure the project is findable by both search engines and AI systems (ChatGPT, Claude, Perplexity, etc.).

> [!info] Why AI Discoverability?
> As AI search grows, traditional SEO is insufficient. AI models need structured descriptions of what a site does, its API capabilities, and its content. The `llms.txt` standard and `ai-plugin.json` format are emerging standards for this.

## Discovery Files

| File | Purpose | Audience |
|---|---|---|
| **llms.txt** | Brief project description for LLMs | ChatGPT, Claude, Perplexity |
| **llms-full.txt** | Detailed project description with all features | AI deep research |
| **llm.md** | Markdown-formatted LLM context | AI models with MD parsing |
| **agents.md** | Agent-friendly description with API details | AI agents (AutoGPT, etc.) |
| **agents.txt** | Plain text agent description | Simpler AI agents |
| **metadata.json** | Schema.org structured data | Google, Bing |
| **ai-plugin.json** | OpenAI plugin manifest format | ChatGPT plugins |
| **robots.txt** | Search engine crawl directives | Googlebot, Bingbot |
| **sitemap.xml** | URL listing for crawlers | Search engines |
| **/docs** | Human-readable documentation page | Developers, users |

## llms.txt

```
# Stocky Terminal
> Open-source Bloomberg alternative for India

## What it does
Stocky Terminal is a browser-based financial terminal providing:
- Live NSE/BSE market data from Zerodha, Dhan, Yahoo Finance
- 27+ layer OSINT geopolitical map (conflicts, disasters, flights, vessels)
- AI-generated trade signals via Groq (Llama 3.3 70B)
- Automated daily market briefs at 8AM/8PM IST
- Options chain with full Greeks for Nifty, BankNifty, Sensex
- 333+ RSS news feeds with sentiment classification
- TradingView charts with 13 candlestick patterns

## URL
https://terminal.stockyai.xyz

## API
30+ REST endpoints. See /docs for full reference.

## Tech Stack
TypeScript, Vite, deck.gl, MapLibre, TradingView Lightweight Charts, Vercel Edge, Upstash Redis, Groq API
```

## metadata.json (Schema.org)

```json
{
    "@context": "https://schema.org",
    "@type": "WebApplication",
    "name": "Stocky Terminal",
    "description": "Open-source Bloomberg alternative for India with live market data, OSINT map, and AI signals",
    "url": "https://terminal.stockyai.xyz",
    "applicationCategory": "FinanceApplication",
    "operatingSystem": "Any (Web Browser)",
    "offers": {
        "@type": "Offer",
        "price": "0",
        "priceCurrency": "USD"
    },
    "author": {
        "@type": "Person",
        "name": "SirCharan",
        "url": "https://github.com/SirCharan"
    },
    "license": "https://www.gnu.org/licenses/agpl-3.0.en.html",
    "isAccessibleForFree": true,
    "browserRequirements": "Modern browser with JavaScript enabled"
}
```

## ai-plugin.json

```json
{
    "schema_version": "v1",
    "name_for_human": "Stocky Terminal",
    "name_for_model": "stocky_terminal",
    "description_for_human": "Open-source Bloomberg alternative for India",
    "description_for_model": "Stocky Terminal provides real-time Indian stock market data, OSINT geopolitical intelligence, AI trade signals, and daily market briefs. Use this to get live NSE/BSE quotes, options chain data, FII/DII flows, and market analysis for Indian equities.",
    "auth": { "type": "none" },
    "api": {
        "type": "openapi",
        "url": "https://terminal.stockyai.xyz/openapi.json"
    },
    "logo_url": "https://terminal.stockyai.xyz/icon-512.png",
    "contact_email": "hello@stockyai.xyz",
    "legal_info_url": "https://terminal.stockyai.xyz/legal"
}
```

## robots.txt

```
User-agent: *
Allow: /
Allow: /blog/
Allow: /docs
Disallow: /api/

Sitemap: https://terminal.stockyai.xyz/sitemap.xml
```

> [!tip] API Exclusion
> The `/api/` path is disallowed in robots.txt to prevent search engines from indexing API responses as web pages. API documentation is available at `/docs` instead.

## sitemap.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <url>
        <loc>https://terminal.stockyai.xyz/</loc>
        <changefreq>daily</changefreq>
        <priority>1.0</priority>
    </url>
    <url>
        <loc>https://terminal.stockyai.xyz/blog</loc>
        <changefreq>daily</changefreq>
        <priority>0.8</priority>
    </url>
    <url>
        <loc>https://terminal.stockyai.xyz/docs</loc>
        <changefreq>weekly</changefreq>
        <priority>0.7</priority>
    </url>
</urlset>
```

> [!warning] Dynamic Blog Posts
> The sitemap currently lists only static pages. Blog posts (daily briefs) are dynamically generated and not in the sitemap. A future improvement would be a dynamic sitemap generator that includes all published brief URLs.

## Related Notes

- [[Deployment]]
- [[Daily Market Brief]]
- [[API Endpoint Reference]]
- [[Project Overview]]
