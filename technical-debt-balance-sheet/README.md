# technical-debt-balance-sheet

**A working balance sheet for one piece of technical debt. Live formulas, sensitivity analysis, yours to use.**

"The codebase is slowing us down" is true and useless, because finance funds numbers, not sympathy. This spreadsheet turns that complaint into the three numbers a CFO can act on: the principal to clear the debt, the interest you pay every year you carry it, and the payback period on a paydown.

It's the companion to **"Technical Debt Is a Balance Sheet Liability, Not a Metaphor"** (Engineering Economics, Part 7). The article makes the argument. This tool lets you run it against your own debt.

> **Download:** [`technical-debt-balance-sheet-calculator.xlsx`](./technical-debt-balance-sheet-calculator.xlsx)

---

## Why this exists

Technical debt stays unfunded because it's invisible on every report leadership reads. There's no P&L row called "slower because the auth module is a swamp." So the cost hides, the debt compounds, and cleanup keeps losing budget fights to features.

Ward Cunningham didn't mean the term as a metaphor. He meant it almost literally: shipping code you know isn't right buys speed now, and you pay interest on every future change until you repay the principal. Principal, interest, a repayment call. That's a loan, and a loan belongs on a ledger.

This calculator builds that ledger for one specific piece of debt. Put in how much time it burns and what it costs to fix, and it hands back the interest, the principal, an implied interest rate, and how fast remediation pays for itself. The point is not precision to the dollar. It's getting the real cost onto the same page as the features it competes with, so the decision gets made with the liability in plain view.

---

## What's in the workbook

Four tabs:

### 1. Start Here
A one-screen orientation: what a technical debt balance sheet is (principal + interest + payback), that blue cells are the only inputs, the tab list, and the honest limits.

### 2. Debt Balance Sheet
The core model. **Edit only the shaded blue cells.** Everything else is a formula.

Inputs:
- **Loaded engineer hourly cost ($)** - salary plus benefits, payroll tax, equipment, and overhead, per hour. Same definition used across every model in the series.
- **Engineers affected by this debt** - how many people routinely route around it.
- **Hours per engineer per sprint lost to this debt** - the time each loses working around it. Default: 4 hours a week over a two-week sprint.
- **Sprints per year** - your cadence. 26 two-week sprints is a full year.
- **Incident-frequency delta per year** and **loaded cost per incident ($)** - extra production incidents you attribute to the debt, and what each one costs fully loaded. Both default to zero so the headline stays on the lost-time cost until you add them.
- **Estimated remediation hours (base)** - engineering hours to clear the debt, before the multiplier. Your honest first guess.
- **Complexity / risk multiplier (x)** - scales remediation for integration, testing, and unknowns. 1.2x for a well-isolated module, 2x or worse for something tangled into everything.

Computed for you:
- **Annual interest ($/yr)**: lost time plus incident cost. What you pay every year until the debt is fixed.
- **Principal to remediate ($)**: remediation hours times loaded rate times the complexity multiplier.
- **Implied annual interest rate**: interest divided by principal, shown as a percent. The yearly return on paying it down.
- **Payback period**, in years and months: principal divided by annual interest.
- A plain-language one-sentence balance sheet that assembles all four into the line you take to finance.

### 3. Debt Ceiling
Given total team capacity (engineers times working hours times sprints), this tab shows what fraction of that capacity the debt's interest already eats, then projects how the fraction climbs as the hours-lost assumption grows. It flags the point where interest approaches total capacity, the ceiling where everyone is flat out and feature velocity drops toward zero. That ceiling is not hypothetical. It's the wall careful teams hit when nearly all their capacity goes to servicing a loan nobody wrote down.

### 4. Sensitivity
The hours-lost-per-sprint number drives the whole result and is the one you are least sure of. This tab sweeps it across a range and reports annual interest, implied interest rate, and payback at each step. If the implied rate and payback barely move, trust the call. If they swing, you've found the one assumption worth going to measure instead of guess.

---

## How to use it

1. Open `technical-debt-balance-sheet-calculator.xlsx` in Excel, Google Sheets, LibreOffice Calc, or Numbers.
2. On **Debt Balance Sheet**, set the blue inputs for one specific piece of debt you want to price.
3. Read the four results: annual interest, principal, implied rate, and payback. The one-sentence balance sheet at the bottom is the version you say out loud to finance.
4. Open **Debt Ceiling**, set your team size and working hours, and see how much of your total capacity the interest already consumes, plus how close the trend is to the ceiling.
5. Open **Sensitivity** and check whether the decision holds as the hours-lost estimate moves. If it flips, that's where your estimation effort belongs.

The defaults reproduce the worked example from the article: a $150/hour loaded rate, six engineers each losing four hours a week to one module, which comes to roughly **$187,000 a year in interest**, against a **$300,000** remediation principal, for a payback inside two years.

---

## The honest limits

- **It prices estimated cost, not certainty.** The interest figure rides on your read of how much capacity the debt eats, which is a judgment call wearing a dollar sign. Present it as a range, show the inputs, and let the finance partner see the assumptions instead of hiding them behind one confident number.
- **Not all debt has measurable interest.** Some debt sits in a corner nobody touches, costing nothing until the day you finally need to change that corner. Aim the balance sheet at the debt you are actively paying interest on, not every imperfection in the codebase.
- **A financial frame can make a soft estimate look like hard fact.** "$1.2 million in debt" takes on a life of its own in a slide deck and gets quoted back as gospel six months later. Keep the ranges visible and the word "estimate" attached.
- **All default numbers are illustrative, from the article.** Replace every blue cell with your own.

---

## Read the full article

**[Technical Debt Is a Balance Sheet Liability, Not a Metaphor](#)** - Engineering Economics, Part 7.
*(Replace this with the published article URL.)*

Part of the Engineering Economics series: why good technical decisions are also financial decisions. This calculator lives in the [engineering-economics-models](../) collection alongside the other models from the series.

---

## License

Released under the [MIT License](../LICENSE). Free to use, copy, and adapt for your own technical debt decisions. Attribution appreciated but not required. No warranty: the numbers are only as good as the assumptions you put in the blue cells.
