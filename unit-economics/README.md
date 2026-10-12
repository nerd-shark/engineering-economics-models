# unit-economics

**A working unit-economics and cost-curve simulator. Live formulas, scale projection, yours to use.**

As your product scales, does cost per unit fall, hold, or rise against revenue per unit? That one question decides whether growth makes you healthier or quietly kills you. This spreadsheet plots your cost and revenue curves from today's volume out to 1000x and flags the volume where margin goes negative.

It's the companion to **"Cost as a Non-Functional Requirement: The Frugal Architect"** (Engineering Economics, Part 3). The article makes the argument. This tool lets you run it against your own product.

> **Download:** [`unit-economics-calculator.xlsx`](./unit-economics-calculator.xlsx)

---

## Why this exists

Werner Vogels' Frugal Architect, Law II: systems that last align cost to the business. The failure mode is a mismatch between how you charge (flat, per-seat) and how your cost scales (per-gigabyte, per-request). The gap widens every time you grow, and revenue keeps going up the whole way, so nobody notices until the margin is gone.

The fix is to make the unit visible, then project it. This tool forces the "what does this cost at 10x?" question that almost no architecture review asks.

---

## What's in the workbook

Four tabs:

### 1. Start Here
Orientation: the three curves, the three tabs, and the honest limits.

### 2. Unit Economics
Today's snapshot. **Edit only the shaded blue cells:** monthly infrastructure spend, units of value per month, price per unit. It computes cost per unit, revenue per unit, gross margin per unit and %, monthly gross profit, and a health check. Confirm margin is positive here before you worry about scale.

### 3. Scale Projection
The 10x question, answered across 1x to 1000x. You set a single **cost-scaling exponent**:

- **< 1 (sublinear):** cost per unit falls as you grow (caching, batching, amortized fixed cost). Growth helps you.
- **= 1 (linear):** cost per unit holds. No scale economy.
- **> 1 (superlinear):** cost per unit rises (coordination overhead, chatty services, data that gets pricier to query). Growth hurts you.

It projects total cost, cost per unit, margin, and gross profit at each scale, names your curve type, and flags the volume where margin goes negative if it does.

### 4. Sensitivity
Sweeps the cost-scaling exponent from 0.7 to 1.2 and shows the margin at 1x / 10x / 100x / 1000x for each. This is the number you're least sure of, so bound it rather than trusting a single value. Read down a column and watch scale turn from reward into collapse as the exponent crosses 1.0.

---

## How to use it

1. Open `unit-economics-calculator.xlsx` in Excel, Google Sheets, LibreOffice Calc, or Numbers.
2. On **Unit Economics**, set your three blue inputs. Confirm the margin is positive.
3. On **Scale Projection**, set the cost-scaling exponent that best matches your architecture. Start at 1.0 (linear) if unsure, then test lower (you cache/batch) and higher (chatty, coordination-heavy).
4. Read the curve type and the margin at 1000x. If it goes negative, you've found a redesign that's far cheaper to do now than later.
5. On **Sensitivity**, bound the exponent and see how much the answer depends on it.

The defaults reproduce the article's document-processing example: $80K/month infra, 40M documents/month, $0.002 cost per unit, $0.005 price, **60% gross margin**.

---

## The honest limits

- **The cost-scaling exponent is an abstraction**, not a measurement. Real architecture doesn't scale on one clean exponent. It's a thinking tool to find roughly which curve you're on; use the Sensitivity tab to bound it.
- **It prices cost against revenue, nothing else.** It says nothing about whether anyone wants the product. Pre-product-market-fit, this is the wrong thing to optimize (that's in the article too).
- **Defaults are illustrative, from the article.** Replace every blue cell with your own.

---

## Read the full article

**[Cost as a Non-Functional Requirement: The Frugal Architect](#)** — Engineering Economics, Part 3.
*(Replace this with the published article URL.)*

Part of the Engineering Economics series: why good technical decisions are also financial decisions. This calculator lives in the [engineering-economics-models](../) collection alongside the other models from the series.

---

## License

Released under the [MIT License](../LICENSE). Free to use, copy, and adapt for your own unit-economics work. Attribution appreciated but not required. No warranty: the numbers are only as good as the assumptions you put in the blue cells.
