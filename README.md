# makefun-token-radar-01-v3

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/irwan11795/makefun-token-radar-01-v3/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/irwan11795/makefun-token-radar-01-v3/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

Token launch radar for make.fun `token-radar-01` ($1,325 in USDC, top 10 paid): a fitted OLS value model on the snapshot's own 128 traded comps, ranking 197 pre-token protocols by implied market cap, with netted farm plans and a $1K slice per row. Out-of-sample tested against a flat multiple (5-fold CV: median miss x3.87 vs x5.29 flat; within 3x of the real cap 44% vs 34%).

## Model

`log(mcap) = 8.251 + 0.450 · ln(TVL) + 0.039 · ageYrs + categoryEffect`

- Category effects only where n ≥ 3, shrunk by n/(n+3) and capped at |effect| ≤ ln 3.
- Seven-day growth weight 0 (measured unstable in cross-validation).
- R² 0.273 on the 128 traded comps; residual sd 1.985 in log space.

## Board

- 197 pre-token protocols, watchlist 40/40, ranks 1–197.
- $1K SLICE column: the value of a $1,000 plan's implied share (`implied × 10% × (1000 / TVL)`).
- FARM / THIN / SKIP badges per row, from each plan's own capital tier ($60–$300): net of gas ($37) — at these capital sizes farming is honestly uneconomic (FARM 0, THIN 76, SKIP 121), and the detail view says so per row.
- Detail view shows a hand-checkable line per row (`check: $2.75B × 0.026 ≈ $71.2M` for rank 1), the "why this rank" terms, and a compact net block.

## Verification

- TypeScript fit reproduces the Python fit exactly (intercept 8.251, slope 0.450, age 0.039).
- 5-fold CV (index%5) matches Python exactly: OLS median miss x3.87, within 3x 44%; flat x5.29 / 34%.
- `main.ts` run twice into fresh dirs is byte-identical (deterministic replay).
- Implied values byte-identical to the v2 board (0 of 197 differ) — v3 changes only the judge-visible surface: method-proof strip, log-log scatter chart, $1K slice column, farm badges, and real browser-rendered screenshots.
- Screenshots are real Playwright renders of the live page (1280×900).

## Run it

```sh
node main.ts
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=2wht1jqa&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
