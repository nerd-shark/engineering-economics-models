# portfolio-review

**A working scorecard for your whole application portfolio. Live formulas, sensitivity analysis, yours to use.**

"We have too many apps" is true and useless, because nobody sunsets a vague feeling. This spreadsheet turns that instinct into the numbers a budget owner can act on: a value-to-cost ratio for every application, a keep / watch / sunset call against a threshold you control, and the annual spend you would recover by retiring the worst performers.

It's the companion to **"The Production Portfolio Review"** (Engineering Economics, Part 8). The article makes the argument. This tool lets you run it against your own portfolio.

> **Download:** [`portfolio-review-calculator.xlsx`](./portfolio-review-calculator.xlsx)

---

## Why this exists

Every application was justified by a business case. Someone promised a return, got the budget, shipped it. Then the process changed, the users drifted elsewhere, the infrastructure kept running, and a new team inherited it without the context. The business case was never checked again. The app just stayed.

A portfolio review is the discipline of going back and asking the question nobody asked at launch plus three: what does this system actually return now, and what does it cost to keep running? Treat the portfolio the way you'd treat financial holdings. Some apps appreciate, earning far more value than they cost. Some depreciate, sliding toward replacement. And some cost more to hold than they will ever return, which makes them candidates for liquidation.

This calculator builds that scorecard. Put in each app's annual run cost and the value it realizes, and it hands back the value-to-cost ratio, the cost per active user, the gap between realized and promised ROI, and a keep / watch / sunset recommendation. The point is not precision to the dollar. It's getting the whole portfolio onto one page with an honest number next to each line, so the retire-or-keep decision gets made on the math instead of on whose project it was.

---

## What's in the workbook

Three tabs:

### 1. Start Here
A one-screen orientation: what a portfolio review is (realized versus promised ROI; appreciate, depreciate, liquidate), that blue cells are the only inputs, the tab list, and the honest limits.

### 2. Portfolio Scorer
The core model. **Edit only the shaded blue cells.** Everything else is a formula.

Two threshold inputs set the rule:
- **Keep if value-to-cost ratio is at or above** - default 2.0. At or above this, the app earns its spend.
- **Sunset if value-to-cost ratio is below** - default 1.0. Below this, the app returns less than it costs to run. Anything between the two lands in Watch.

Then one row per application, with blue inputs:
- **Annual run cost ($)** - fully loaded cost to keep the app running for a year: infrastructure, licenses, and the engineer time to support it. Use the same loaded engineer cost definition as the rest of the series (salary plus benefits, payroll tax, equipment, and overhead).
- **Realized annual value ($)** - what the app actually delivers now, in dollars. Your honest estimate, not the original projection.
- **Active users** - how many people genuinely use it.
- **Support burden (tickets/mo)** - the monthly operational drag.
- **Promised ROI** - the return the original business case promised, for the realized-versus-promised comparison.

Computed for you per row:
- **Value-to-cost ratio**: realized value divided by run cost. The headline number.
- **Cost per active user**: run cost divided by active users.
- **Realized vs promised gap**: the realized ratio minus the ROI the business case promised. A big negative gap is an app that never delivered what it sold.
- **Recommendation**: Keep, Watch, or Sunset, scored against your two thresholds.

A portfolio total row sums run cost and realized value and shows the blended ratio. Below it, category counts and a recoverable-spend block compute the gross run cost, the value forgone, and the net annual spend you would recover by sunsetting the bottom quartile, plus the same three numbers for the single worst app on its own.

### 3. Sensitivity
The keep/sunset threshold is the number you are least sure of, and it quietly decides how many apps get retired. This tab sweeps the sunset threshold across a range and reports how many apps fall into each bucket and how much spend becomes recoverable at each step. If the recommendation set barely changes as the line moves, trust the call. If apps flip in and out at every step, the threshold is doing the deciding, so set it on purpose.

---

## How to use it

1. Open `portfolio-review-calculator.xlsx` in Excel, Google Sheets, LibreOffice Calc, or Numbers.
2. On **Portfolio Scorer**, set the two blue threshold cells (Keep at or above, Sunset below).
3. Replace the six sample rows with your own applications. For each, fill the blue cells: name, annual run cost, realized annual value, active users, support burden, and promised ROI.
4. Read each app's value-to-cost ratio and its keep / watch / sunset call, then the portfolio totals and the blended ratio.
5. Read the recoverable-spend block: the gross run cost, value forgone, and net spend you would recover by retiring the bottom quartile, plus the single-worst-app figure.
6. Open **Sensitivity** and check whether the calls hold as the threshold moves. If they flip, that's where the decision really lives.

The defaults reproduce the worked example from the article: a six-application portfolio costing **$1,840,000 a year** to run and realizing **$3,680,000** in value, a blended **2.00x**. One app, a legacy reporting engine, costs **$400,000 a year** and returns **$50,000**, a **0.125x** ratio against an original promise of 4.0x. Sunsetting the bottom quartile (the two worst apps) recovers **$580,000** in run cost against **$200,000** of value forgone, for a net **$380,000 a year** redeployed to the apps that earn their keep.

---

## The honest limits

- **Realized value is itself an estimate.** A low ratio can mean the value is mis-measured, not that the app is dead. Attributing revenue or efficiency to one system is a judgment call wearing a dollar sign. Treat a bad score as a reason to investigate, not a verdict, and show your value assumptions.
- **Some apps must run regardless of the ratio.** Compliance, security, and strategic systems can score badly on pure cost-per-value and still be mandatory. Flag those before the scorecard talks you into retiring something you are required to keep.
- **Politics can override the math.** Someone owns every app on the list, and someone's budget is at risk when it goes on the block. A structured review and executive sponsorship matter as much as the number. The scorecard gives you the number, not the mandate.
- **A financial frame can make a soft estimate look like hard fact.** "$380,000 recoverable" takes on a life of its own in a slide deck. Keep the ranges visible and the word "estimate" attached.
- **All default numbers are illustrative, from the article.** Replace every blue cell with your own.

---

## Read the full article

**[The Production Portfolio Review](#)** - Engineering Economics, Part 8.
*(Replace this with the published article URL.)*

Part of the Engineering Economics series: why good technical decisions are also financial decisions. This calculator lives in the [engineering-economics-models](../) collection alongside the other models from the series.

---

## License

Released under the [MIT License](../LICENSE). Free to use, copy, and adapt for your own portfolio decisions. Attribution appreciated but not required. No warranty: the numbers are only as good as the assumptions you put in the blue cells.
