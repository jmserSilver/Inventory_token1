# Inventory Review Dashboard

A single-file, browser-based inventory and warehouse operations dashboard. No build step, no server, no install — download `index.html` and open it in any modern browser.

It opens with fictional sample data so you can explore right away, and you can load your own CSV. Your file is read in the browser only; nothing is uploaded or saved.

## Features

**Stock**
- **Overview** – stock vs. days-of-supply target, top shortages, replenishment health, movements and write-offs, and auto-generated key observations
- **Category View** – scorecard per category (deviation, days of supply, turns, fill rate, stockouts, excess)
- **Item View** – searchable, sortable, filterable item list with CSV export and per-item detail drawer
- **Movements** – monthly receipts vs. issues, write-offs by reason, fastest and slowest movers

**Warehouse operations** (simulated sample data)
- **Warehouse Layout** – floor plan heatmap (occupancy / pick activity), ABC slotting analysis, capacity and utilisation trend
- **Inbound** – dock door Gantt schedule, truck arrivals, receiving and putaway backlog
- **Dispatch** – outbound dock schedule and route plan, order pipeline and pick waves, fleet load fill

**Cost** – carrying cost, value by age, write-offs by month, value by category and warehouse

Also: warehouse filter, at-cost / at-retail valuation toggle, light and dark mode, and a mobile-friendly layout.

## Quick start

1. Download `index.html` (or clone the repo).
2. Open it in Chrome, Edge, Firefox or Safari.
3. Click **Load data** to use your own CSV, download a blank template, or reset to the sample data.

## CSV format

One row per item per warehouse.

| Column | Required | Description |
|---|---|---|
| `sku` | ✓ | Item code |
| `name` | ✓ | Item name |
| `category` | ✓ | Category |
| `warehouse` | ✓ | Warehouse / location |
| `unit_cost` | ✓ | Cost per unit |
| `unit_price` | ✓ | Selling price per unit |
| `on_hand` | ✓ | Units in stock |
| `reorder_point` | ✓ | Reorder point (units) |
| `avg_daily_demand` | ✓ | Average units issued per day |
| `on_order` | ✓ | Units on open purchase orders |
| `inbound_eta` | ✓ | Expected arrival date (`YYYY-MM-DD`), blank if none |
| `age_days` | ✓ | Average age of stock in days |
| `fill_rate` | | 0–1 |
| `wo_reason` | | Main write-off reason |
| `rec_jan` … `rec_dec` | | Monthly receipts (units) |
| `iss_jan` … `iss_dec` | | Monthly issues (units) |
| `wo_jan` … `wo_dec` | | Monthly write-offs (units) |

Without the monthly history columns, the Movements cards stay empty.

> Note: the Warehouse Layout, Inbound and Dispatch views always show simulated data; they are not driven by the CSV.

## Configuration

Targets and thresholds live at the top of the `<script>` in `index.html`:

```js
const AS_OF = new Date(2026, 9, 31); // data as-of date
const TARGET_DOS = 35;               // target days of supply
const EXCESS_DOS = 120;              // above this = excess stock
const AGED_DAYS = 180;               // older than this = aged stock
const CARRY_RATE = 0.24;             // annual carrying cost, share of value
```

## Tech

Plain HTML, CSS and vanilla JavaScript with hand-drawn SVG charts. The only external request is the Google Fonts stylesheet (Plus Jakarta Sans); it falls back to system fonts offline.

## License

[MIT](LICENSE) © 2026 Lucas
