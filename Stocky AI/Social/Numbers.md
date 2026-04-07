---
tags:
  - stocky-ai
  - social
  - metrics
created: 2026-04-07
status: complete
---

# Numbers

> [!info] Key metrics for conversations, interviews, and pitches

## Build Metrics

| Metric | Value |
|--------|-------|
| Total commits | 79 |
| Build period | 60 days |
| Deploy frequency | 1.3/day (auto-deploy on push) |
| Last updated | March 2026 |

## Scale Numbers

| Metric | Value |
|--------|-------|
| Frontend components | 50+ |
| Card components | 27 (dynamically imported) |
| Backend handlers | 31 |
| API endpoints | 40+ |
| Database tables | 14 |
| Feature buttons | 20 |

## LLM Numbers

| Metric | Value |
|--------|-------|
| LLM models | 4 (Llama 3.3 70B, Scout 17B, GPT-OSS 120B, Gemini 2.5 Pro) |
| Groq API keys | 6 (round-robin) |
| Effective RPM | 180 (6 keys x 30 RPM) |
| LLM cost | $0 (free tier) |
| Agent architectures | 3 (Triad-3, Crew-7, Council-6) |
| Button-specific prompts | 16 |
| Max agents per query | 7 (Crew) or 6 (Council, 3 rounds) |

## Data Numbers

| Metric | Value |
|--------|-------|
| RSS news sources | 41 (8 categories) |
| Dhan securities mapped | 73 |
| Cache TTL range | 10s - 3600s |
| Positive sentiment keywords | 25 |
| Negative sentiment keywords | 25 |
| Regex intent patterns | 30+ |

## Performance Numbers

| Metric | Value |
|--------|-------|
| Regex intent parsing | <1ms |
| AI intent parsing | 200-500ms |
| Quick analysis | 1-3s |
| Deep 3-stage pipeline | 5-12s |
| Council 6-agent debate | 15-30s |
| JS bundle reduction (dynamic imports) | ~35% |
| Boot screen skip (returning users) | 0ms vs 4.2s |

## CK Portfolio Numbers

| Metric | Value |
|--------|-------|
| Stock portfolio ROI | 100%+ in 9 months |
| Capital deployed | 15L |
| Win rate | 73% |
| MF XIRR | >50% |

## Target Scale (Future)

| Metric | Current | Target |
|--------|---------|--------|
| RPS | ~10 | 10,000 |
| Concurrent users | 1 | 50,000 |
| Data volume | ~50 MB | 10 TB |
| Database QPS | ~100 | 50,000 |
| LLM cost/query (at scale) | $0 | $0.001 (self-hosted) |

## Related Notes
- [[Interview Prep]]
- [[Pitch]]
- [[Architecture]]
