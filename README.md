# QDM v0.4.1 forward ledger

A public, append-only forward record of the **raw** direction shown by the TradingView indicator
"QDM Ordered Timeframe Checklist [crypto perps]" (frozen research build v0.4.1).
It is a record, not a performance promise and not financial advice.

- Lanes: Gate USDT perpetuals BTC, ETH and SOL on 15m, 1h and 4h. Data comes from the public Gate API, closed bars only.
- Start: 2026-10-14. Nothing earlier is backfilled.
- `ledger/*_predictions.csv`: one row per closed bar with direction (+1, 0 or -1), p_up, analog counts, Wilson 95% interval and the time it was recorded.
  - `late=1` means the row was written after the next bar had closed, for example after a PC outage. It is still computed from past data only, but it is not a real-time proof.
- `ledger/*_outcomes.csv`: the realized 5-bar return, appended once the exit bar has closed.
- `STATS.md`: counts non-overlapping calls only and subtracts a 0.25% round-trip cost.
  - A lane passes only with at least 30 calls and a net-hit Wilson lower bound above 50%.
- Rows are never edited. Each daily commit time is part of the record.
- Parity between this ledger and the TradingView table is checked by hand and noted in STATS.md once done. Until then it is not verified.

As of the start, historical validation passed on 0 of 18 lanes, so the indicator's arrows and alerts stay locked.
