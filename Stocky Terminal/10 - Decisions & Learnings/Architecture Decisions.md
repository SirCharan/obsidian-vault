---
title: Architecture Decisions
date: 2026-04-07
tags:
  - stocky-terminal
  - adr
  - architecture-decisions
  - tradeoffs
status: published
category: decisions
---

# Architecture Decisions

This note documents the key architectural decisions made during Stocky Terminal's development, including the reasoning and tradeoffs for each.

> [!info] Decision Record Format
> Each decision follows the format: **Context** (why the decision was needed), **Decision** (what was chosen), **Consequences** (tradeoffs accepted).

## ADR-001: Zero Frameworks (Vanilla TypeScript)

**Context:** The terminal needs to render 12+ panels with real-time data updates at 15-second intervals. Framework overhead (virtual DOM diffing, component lifecycle) adds latency to every update cycle.

**Decision:** Use vanilla TypeScript with direct DOM manipulation, a custom Panel base class, and targeted patching (patchTableRows pattern).

**Consequences:**
- Positive: Sub-50ms interaction latency, tiny bundle size, no framework churn
- Positive: Contributors need only TypeScript + DOM APIs (universal skills)
- Negative: No component ecosystem (no ready-made dropdown, modal, tooltip libraries)
- Negative: Manual state management (AppContext singleton vs. Redux/Zustand)
- Negative: More boilerplate for common UI patterns

> [!tip] Validation
> After 6 months and 45+ features, the zero-framework approach has held up well. The most complex UI (options chain table, OSINT map) would not have been simpler with React — they rely on canvas/WebGL rendering regardless.

## ADR-002: Groq Over OpenAI

**Context:** AI features need an LLM for signal generation, brief writing, and analysis. Options: OpenAI GPT-4, Anthropic Claude, Groq-hosted Llama, self-hosted Ollama.

**Decision:** Use Groq's hosted Llama 3.3 70B Versatile as primary, Ollama as local fallback.

**Consequences:**
- Positive: 500+ tokens/second (10x faster than GPT-4)
- Positive: Generous free tier (sufficient for current usage)
- Positive: Open-source model (Llama) — no vendor lock-in on the model itself
- Negative: Groq's free tier has rate limits that could be hit at scale
- Negative: Llama 3.3 70B is slightly less capable than GPT-4 on complex reasoning
- Negative: Groq is a younger company — reliability track record is shorter

## ADR-003: Vercel Edge Functions

**Context:** Need a serverless backend for 30+ API endpoints with global deployment, low latency, and minimal ops burden.

**Decision:** Vercel Edge Functions for all API endpoints and cron jobs (via GitHub Actions triggering edge function URLs).

**Consequences:**
- Positive: ~0ms cold start (V8 isolates, not containers)
- Positive: Global edge deployment (IAD, SIN, BOM)
- Positive: Zero ops — no server provisioning, scaling, or monitoring
- Positive: Tight integration with Git push-to-deploy
- Negative: No WebSocket support (blocking Phase 3 real-time feature)
- Negative: 30-second execution limit (sufficient for current endpoints, but backtesting may need longer)
- Negative: No persistent connections to upstream APIs

## ADR-004: Upstash Redis (No Traditional Database)

**Context:** Need server-side storage for blog posts, AI insights, signals, subscriber list, and ratings. Options: PostgreSQL, MongoDB, Redis, DynamoDB.

**Decision:** Upstash Redis as the sole server-side data store.

**Consequences:**
- Positive: Sub-millisecond read/write latency
- Positive: Serverless pricing (pay per request)
- Positive: Native TTL support (perfect for cache-heavy architecture)
- Positive: Sorted sets for blog posts (natural ordering by edition number)
- Negative: No relational queries (can't JOIN subscribers with ratings easily)
- Negative: Memory-based pricing can get expensive at scale
- Negative: No built-in backup/restore (Upstash provides snapshots, but no PITR)

> [!warning] Scale Concern
> At 70 subscribers, Redis works perfectly. At 10,000 subscribers, the `SMEMBERS` call to fetch all subscriber emails would return a large set. The email sending loop would need to be refactored to use `SSCAN` for pagination and a proper job queue.

## ADR-005: deck.gl for OSINT Map

**Context:** Need to render 27+ data layers with potentially thousands of points (conflict events, earthquakes, flights) at 60fps.

**Decision:** deck.gl + MapLibre GL JS.

**Consequences:**
- Positive: WebGL-accelerated rendering — handles millions of points
- Positive: MapLibre is open-source (no Mapbox pricing)
- Positive: deck.gl's layer system maps cleanly to OSINT data categories
- Positive: Reusable for Phase 2 IV surface (3D rendering)
- Negative: Large bundle (~120kB gzipped) — requires lazy loading
- Negative: Steep learning curve for contributors
- Negative: Mobile GPU performance can be poor with all layers active

## ADR-006: Vanilla CSS (No CSS Framework)

**Context:** Need consistent styling across 12+ panels with dark/light theming.

**Decision:** Plain CSS with CSS Custom Properties for theming. No Tailwind, no styled-components, no CSS modules.

**Consequences:**
- Positive: Zero CSS build step, instant HMR
- Positive: CSS Custom Properties make theming trivial
- Positive: Full control over specificity and cascade
- Positive: Cacheable CSS files (no CSS-in-JS runtime)
- Negative: No utility classes (more verbose for common patterns)
- Negative: No automatic dead CSS elimination
- Negative: Potential for selector conflicts (mitigated by panel-scoped selectors)

## Decision Matrix Summary

| Decision | Primary Driver | Risk Level | Revisit Trigger |
|---|---|---|---|
| Zero frameworks | Performance | Low | If contributor onboarding becomes bottleneck |
| Groq over OpenAI | Speed + cost | Medium | If Groq reliability drops below 99% |
| Vercel Edge | Developer experience | Medium | When WebSocket is needed (Phase 3) |
| Upstash Redis only | Simplicity | Medium | At 5,000+ subscribers |
| deck.gl | Performance | Low | If WebGPU becomes viable alternative |
| Vanilla CSS | Simplicity | Low | If design system is formalized |

## Related Notes

- [[Tech Stack]]
- [[System Architecture]]
- [[Frontend Architecture]]
- [[Technical Learnings]]
- [[Future Roadmap]]
