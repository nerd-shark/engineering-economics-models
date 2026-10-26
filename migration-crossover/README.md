# migration-model

**A working crossover calculator for the migrate-or-wait decision. Live formulas, sensitivity analysis, yours to use.**

Keeping an aging system is cheaper than migrating every single year, right up to and past the point where it isn't. This spreadsheet finds that point: the crossover year when the cumulative cost of keeping the old system passes the cumulative cost of replacing it.

It's the companion to **"The Economics of Migration: Sunk Cost vs. Rip-and-Replace"** (Engineering Economics, Part 6). The article makes the argument. This tool lets you run it against your own system.

> **Download:** [`migration-crossover-calculator.xlsx`](./migration-crossover-calculator.xlsx)

---

## Why this exists

The "one more year" trap catches careful teams because deferral is locally rational. Every year, maintaining the old system is cheaper than the one-time migration, so you defer. And you're right to, each time, until you're suddenly not. Both numbers climb while you wait: maintenance rises as the system rots, and the migration gets pricier as the system tangles into everything around it.

The trap is that the per-year comparison keeps saying "defer" long after the cumulative comparison says you should already be gone. This calculator plots the cumulative lines so the crossover year stops hiding.

Sunk cost is deliberately absent from the model. Money already spent is gone under every option, so it never appears. Only forward-looking costs move the answer.

---

## What's in the workbook

Four tabs:

### 1. Start Here
A one-screen orientation: what the crossover is, why sunk cost is excluded, the three tabs, and the honest limits.

### 2. Crossover Calculator
The core model. **Edit only the shaded blue cells.** Everything else is a formula.

Inputs:
- **Time horizon (years)** — how far to project (7 to 10 is usually enough).
- **Current annual maintenance of old system ($)** — what keeping it running costs this year.
- **Annual maintenance growth rate (%)** — how fast that cost rises as the system ages (10 to 20% is common for genuinely aging systems).
- **One-time migration cost ($)** — the full replacement cost: build + dual-run + data migration + integration + retraining + testing.
- **Migration realism multiplier (x)** — set to 2.0 to apply the article's 2x rule of thumb to an engineering-only estimate, or 1.0 if your number is already honest.
- **New system annual run cost ($)** — what the replacement costs to operate each year once live.

Computed for you:
- A year-by-year table of annual maintenance, cumulative KEEP, cumulative REPLACE, which is cheaper so far, and the running gap.
- The **crossover year**, detected automatically: the first year cumulative KEEP passes cumulative REPLACE.
- A plain-language interpretation ("migrate by year N", or "keeping still wins across your horizon").

### 3. Hidden Costs of Not Migrating
The KEEP line is never just the maintenance invoice. This tab adds the four hidden costs the article argues for, as editable annual figures:

- Talent attrition / premium to staff legacy skills
- Security exposure (risk-weighted)
- Opportunity cost of the maintenance capacity
- Competitive / feature-velocity drag

It re-runs the crossover with the hidden tax folded into the KEEP line and reports the crossover year **with** and **without** it. The gap between the two is the cost of pretending that keeping the old system is free. With the illustrative defaults, the hidden tax pulls the crossover from year 4 all the way in to year 2.

### 4. Sensitivity
The maintenance growth rate drives the whole result and is the number you are least sure of. This tab sweeps it from 5% to 40% and reports the crossover year at each. If the crossover barely moves, the uncertainty isn't your problem and you can trust the call. If it swings, you've found the one assumption worth going to measure instead of guess.

---

## How to use it

1. Open `migration-crossover-calculator.xlsx` in Excel, Google Sheets, LibreOffice Calc, or Numbers.
2. On **Crossover Calculator**, set the six blue inputs for the system you're deciding about.
3. Read the year-by-year table and the crossover year at the bottom. That year is your decision deadline.
4. Open **Hidden Costs of Not Migrating**, fill in the four blue annual figures, and compare the crossover with and without them. This is the honest version of the "keep" cost.
5. Open **Sensitivity** and check whether the crossover year holds as the growth rate moves. If it flips, that's where your estimation effort belongs.

The defaults reproduce the worked example from the article (current maintenance $600K, rising 20%/yr; $2M migration; $150K/yr new system), which crosses over at **year 4**.

---

## The honest limits

- **It prices cost, not value or execution risk.** A migration that pencils out and is executed badly (see TSB in the article: a forced big-bang cutover that cost roughly £330M) is worse than not migrating. The spreadsheet cannot tell you whether your team can land it. That question deserves as much honesty as the numbers.
- **The maintenance growth rate drives everything and is the hardest to predict.** That's what the Sensitivity tab is for. If the decision flips across a plausible range, go measure the number.
- **Value is real but not modeled.** "The new system lets us ship three times faster" is often the decisive factor and doesn't fit in a cell. Name it explicitly alongside the cost output; don't let its absence from the sheet mean its absence from the decision.
- **All default numbers are illustrative, from the article.** Replace every blue cell with your own.

---

## The real-world version of this trap

The article anchors the model to a real case: the IRS **Individual Master File**, assembly-era code first stood up in the early 1960s and still the authoritative record for US individual tax accounts. The IRS has been trying to replace it for decades. The first attempt (CADE) was scrapped in 2009; its successor (CADE 2) has run for well over a decade with the cost, schedule, and scope revised repeatedly, and completion estimates in the $2.3 to $2.7 billion range. Every one of those deferrals looked locally reasonable. In aggregate they are a multi-decade, multi-billion-dollar demonstration that the crossover doesn't wait for you to feel ready, and that circling it only makes the eventual replacement more expensive. (Sources: GAO-19-471, GAO-22-104387, CRS IF12525.)

---

## Read the full article

**[The Economics of Migration: Sunk Cost vs. Rip-and-Replace](https://medium.com/@the-architect-ds/the-economics-of-migration-sunk-cost-vs-rip-and-replace-8a360c692004)** — Engineering Economics, Part 6.

Part of the Engineering Economics series: why good technical decisions are also financial decisions. This calculator lives in the [engineering-economics-models](../) collection alongside the other models from the series.

---

## License

Released under the [MIT License](../LICENSE). Free to use, copy, and adapt for your own migrate-or-wait decisions. Attribution appreciated but not required. No warranty: the numbers are only as good as the assumptions you put in the blue cells.
