---
tags:
  - stocky-ai
  - engineering
  - trading
created: 2026-04-07
status: complete
---

# Trading Integration

## Broker APIs

| Broker | API | Purpose |
|--------|-----|---------|
| **Zerodha Kite Connect** | kiteconnect SDK | Order placement, portfolio, holdings, margins |
| **Dhan HQ** | REST API v2 (httpx) | Live quotes, OHLC, option chains, historical data |

## Kite Connect Integration

**Config** (from `config.py`):
- `KITE_API_KEY`, `KITE_API_SECRET`, `KITE_USER_ID`, `KITE_PASSWORD`, `KITE_TOTP_SECRET`
- Token stored in SQLite `kite_session` table + in-memory
- Auto-renewal via 24-hour background task with TOTP generation

**Trading endpoints**:
- `/api/kite/login` -- Initiate Kite login flow
- `/api/kite/status` -- Check current session status
- `/api/trade/confirm` -- Execute confirmed trade

## Dhan HQ Integration

**Config**: `DHAN_CLIENT_ID`, `DHAN_ACCESS_TOKEN`
- **73 securities mapped** to Dhan security IDs
- Token auto-renewal every 20 hours
- Fallback chain: Memory -> DB -> API renewal -> env var

**Endpoints used**:
- `/marketfeed/ltp` -- Live last traded price
- `/marketfeed/ohlc` -- Open/High/Low/Close
- `/optionchain` -- Full option chain data
- `/optionchain/expirylist` -- Available expiries
- `/charts/historical` -- Historical candle data

## 2-Phase Trade Execution

> [!warning] Safety: No trade executes without explicit confirmation
> This prevents accidental trades from ambiguous chat messages.

### Phase 1: Intent Capture
1. User says "buy 10 RELIANCE"
2. Intent parser extracts: `{intent: "buy", args: ["RELIANCE", 10]}`
3. Backend creates `pending_action` in database with unique `action_id`
4. Returns `TradeConfirmation` card to frontend

### Phase 2: Explicit Confirmation
1. Frontend shows `TradeConfirmation` card with:
   - Symbol, quantity, estimated price
   - Estimated total value
   - Risk gauge visualization
2. User clicks "Confirm" button
3. Frontend sends `{action_id, action: "confirm"}` to `/api/trade/confirm`
4. Backend executes via Kite API
5. Returns order result card

### Trade Data Model

```
pending_actions:
  - action_id (unique)
  - username
  - action_type (buy/sell/sl)
  - action_data (JSON: symbol, qty, price, product)
  - status (pending/confirmed/cancelled/executed/failed)
```

## Related Notes
- [[Security]]
- [[Backend Stack]]
- [[Architecture]]
