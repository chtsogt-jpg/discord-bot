---
name: exchange-rate
description: Convert between currencies using live exchange rates. Trigger when user asks about currency conversion, exchange rates, or "how much is X in Y".
---

# Exchange Rate Skill

Convert amounts between currencies using live rates. Default home currency is **MNT (Mongolian Tögrög)** since the user is based in Mongolia.

## When to trigger

- "How much is 100 USD in MNT?"
- "Convert 500 EUR to JPY"
- "What's the USD to MNT rate today?"
- "Exchange rate for [currency]"

## Instructions

1. Parse **amount**, **source currency**, and **target currency** from the request. If any is missing:
   - Missing amount → assume 1 of the source currency
   - Missing target → default to MNT (or USD if source is MNT)
   - Missing source → ask the user
2. Fetch live rates via WebFetch. Good sources:
   - https://open.er-api.com/v6/latest/USD (free, no key)
   - https://api.exchangerate.host/latest
   - Google Finance search as fallback
3. Always fetch fresh — never use cached/remembered rates.
4. Report:
   - **Converted amount** (rounded sensibly — MNT no decimals, USD/EUR two decimals)
   - **Rate used**
   - **Timestamp** of the rate
5. If converting to/from MNT and the source doesn't have MNT directly, do two-step via USD.

## Edge cases

- **Unknown currency code** — ask the user to clarify (e.g. "do you mean CNY Chinese Yuan?").
- **API down** — try a second source; if both fail, tell the user rates are temporarily unavailable.
- **Crypto** (BTC, ETH) — supported if the API provides it; otherwise note that you only handle fiat.

## Output format

```
**[Amount] [SRC] = [Converted] [TGT]**
Rate: 1 [SRC] = [rate] [TGT]
As of: [timestamp]
```
