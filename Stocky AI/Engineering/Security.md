---
tags:
  - stocky-ai
  - engineering
  - security
created: 2026-04-07
status: complete
---

# Security

## HTTP Security Headers (next.config.ts)

| Header | Value | Purpose |
|--------|-------|---------|
| Content-Security-Policy | `default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval' googleapis tradingview jsdelivr; connect-src 'self' *.stockyai.xyz *.railway.app analytics` | XSS mitigation |
| X-Frame-Options | DENY | Clickjacking prevention |
| X-Content-Type-Options | nosniff | MIME sniffing prevention |
| X-XSS-Protection | 1; mode=block | Legacy XSS filter |
| Referrer-Policy | strict-origin-when-cross-origin | Referrer leakage prevention |

## CORS Configuration

From `config.py`:
```python
ALLOWED_ORIGINS = [
    o.strip()
    for o in os.environ.get("ALLOWED_ORIGINS", "http://localhost:3000").split(",")
    if o.strip()
]
```

## Auth & Token Management

| Token | Storage | Renewal | Lifetime |
|-------|---------|---------|----------|
| JWT (web) | localStorage | Manual | 30 days |
| Kite access | SQLite + memory | Auto (24h background task, TOTP) | 24 hours |
| Dhan access | SQLite + memory | Auto (20h background task, API renewal) | 24 hours |

- JWT secret: `secrets.token_urlsafe(32)` or env var `WEB_SECRET_KEY`
- JWT encoding: python-jose (HS256)

## 2-Phase Trade Safety

See [[Trading Integration]] for full details. Key safety: no trade executes without explicit Phase 2 confirmation via `pending_actions` table.

## Known Security Gaps

> [!warning] Intentional gaps -- personal tool, not multi-tenant

| Gap | Risk | Current Mitigation |
|-----|------|-------------------|
| JWT in localStorage | XSS can steal token | Single-user tool; CSP reduces XSS surface |
| No CSRF tokens | Cross-site request forgery | CORS allowlist + SameSite cookies (future) |
| SQLite file access | No encryption at rest | Railway volume isolation |
| Hardcoded user "CK" | No multi-tenant auth | Personal tool by design |
| `unsafe-inline` in CSP | Inline script execution | Required by TradingView widget |
| `unsafe-eval` in CSP | eval() allowed | Required by TradingView widget |

## Related Notes
- [[Trading Integration]]
- [[Tradeoffs]]
- [[Architecture]]
