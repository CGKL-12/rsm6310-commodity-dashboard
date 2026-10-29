# ATLAS · RSM6310 Commodity Trading Dashboard

A responsive React + Vite website for the RSM6310 Fall 2026 virtual hedge fund project. Free-tier friendly deployment to Vercel. **No live market data, trade execution, backend, or brokerage integration.**

## Features
- Month and list views with filtering and selected-event research notes, ET timezone.
- Three commodity-related investment theses: Energy Futures; Gold/Copper Macro Futures; Commodity-Linked Equity Options.
- Trade journal: add / edit / delete, open vs closed trades, long or short, fees, stop prices, multipliers, CSV export.
- Risk analytics: realized P&L, closed-trade P&L line chart, hit rate, profit factor, realized drawdown estimate, planned open stop-distance risk, strategy attribution, editable limits.
- Interactive course-requirements checklist.
- Local browser persistence and JSON backup / restore.

## Run locally
Requires Node.js 20 or later.

```bash
npm install
npm run dev
```

Open the address displayed by Vite (usually http://localhost:5173).

## Publish on Vercel
1. Create a new GitHub repository, then upload or push **all files from this folder** (not the enclosing ZIP).
2. In https://vercel.com/new import the GitHub repository.
3. Framework preset: `Vite`; build command: `npm run build`; output directory: `dist`.
4. Select **Deploy**. Your Vercel URL can be shared publicly. Changes pushed to your connected GitHub branch redeploy automatically.

CLI alternative: `npx vercel` (requires Vercel login).

## IMPORTANT: data sharing model
Trade entries, fund settings, and checklist status are stored **only in the localStorage of the browser that entered them**. Publishing a site does NOT synchronize journal entries across teammates. When a teammate opens the URL on a separate browser/device, they will see the public event calendar and strategy playbook, but an empty journal until they import the **JSON backup** someone shares. Use **Backup JSON** and **Import backup** for manual handoffs, or add authentication + a database (e.g. Supabase) for real shared collaboration. Do not upload confidential real financial account data.

## Trade P&L convention
One journal row represents one outright position or **one leg** of a complex option strategy.

`Realized P&L = sign(side) × (exit - entry) × quantity × contract multiplier - total fees`.

- For standard CL futures a commonly used multiplier is 1,000 barrels; verify contract-specific multipliers (and for options, share multipliers) with your venue.
- No prices are fetched automatically. For an open trade, unrealized P&L is not calculated.
- `Open stop-distance exposure = |entry - stop| × quantity × multiplier` for open trades with a stop; **not** a guaranteed or maximum loss; misses gaps, slippage, portfolio correlations, margin, option nonlinearities.
- Max drawdown is measured from the accumulated **closed-trade P&L series**, not daily fund NAV.
- The dashboard does not know your StockTrak positions; manual entries are required.

## Sources and verification
- RSM6310 Project Description PDF supplied by the project team: 3 ideas, derivatives usage, 5 options strategies / 5 equity underlyings, 65 formal trades, formal end Nov 17, presentation / slides Nov 19 & 26.
- BLS release calendar: https://www.bls.gov/schedule/2026/11_sched_list.htm
- EIA weekly petroleum schedule: https://www.eia.gov/petroleum/supply/weekly/schedule.php
- USDA WASDE: https://www.usda.gov/oce/commodity/wasde
- EIA natural gas storage: https://www.eia.gov/naturalgas/storage/

Some EIA natural-gas event slots are explicitly tagged **Verify schedule**: verify their exact times before publishing trading signals. Dates are **not live synced**. Futures/option strategies are hypothetical research examples, not recommendations or proof that coursework requirements have already been fulfilled.

## Files
- `src/data.js`: event schedule, strategy descriptions, project checklist.
- `src/main.jsx`: interactive UI, journal, risk formulas, persistence.
- `src/style.css`: responsive visual design.
- `vercel.json`: SPA routing and build settings.

## Course use
For educational purposes only, not investment advice. Source/course text remains governed by the course's own rules.
