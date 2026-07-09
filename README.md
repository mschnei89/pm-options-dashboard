# Prediction Markets vs Options — live dashboard

A read-only dashboard comparing the risk-neutral probability **P(S_T > K)** implied
by two venues:

- **Polymarket** — the YES price of "will *asset* finish above $K?" *is* that probability.
- **Options (Schwab chains)** — a model-free Breeden–Litzenberger digital,
  `Q(S_T > K) = -e^{rT} dC/dK`, off the out-of-the-money wing.

## View it

**→ https://mschnei89.github.io/pm-options-dashboard/**

Open the link — no install needed. Two views: a **Detail** page (calibration
scatter, per-market probability curve, biggest divergences, per-strike history)
and an **Overlay grid** of every market. A **time slider** (with ▶ play) scrubs
through every snapshot in the data.

## What's here

| File | Purpose |
|------|---------|
| `index.html` | the dashboard (self-contained; vanilla JS, no dependencies) |
| `results/panel/pm_vs_options_panel_LIVE.csv` | the panel it reads: one row per (snapshot, asset, expiration, strike) |

The page fetches the CSV on load, so this is a **hosted snapshot** — it reflects the
data as of the last push, not a real-time feed. Re-push the CSV to update it.

## Columns

`snapshot_ts_utc, asset, expiration, tier, schwab_symbol, strike, pm_yes,
pm_n_ticks, pm_asof, opt_prob, spot, diff, liquid` — where `pm_yes` is the
Polymarket probability, `opt_prob` the option-implied one, and `diff = pm_yes − opt_prob`.
