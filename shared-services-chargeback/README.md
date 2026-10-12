# shared-services-chargeback

**A working chargeback allocator for shared services. Live formulas, cross-subsidy analysis, yours to use.**

Somebody has to pay for the shared Kafka cluster. How you split it (equally, by usage, or absorb it centrally) changes how teams behave. This spreadsheet shows each team's bill under all three methods side by side, and the cross-subsidy that "split equally" quietly creates: how much the light users overpay to cover the heavy ones.

It's the companion to **"Cloud Cost Allocation as Architecture: Your Bill Is an X-Ray"** (Engineering Economics, Part 4). The article makes the argument. This tool lets you run it against your own shared services.

> **Download:** [`shared-services-chargeback-calculator.xlsx`](./shared-services-chargeback-calculator.xlsx)

---

## Why this exists

Shared services (Kafka, logging, observability) cost real money and have no single owner. The three ways to split that cost have very different incentives:

- **Split equally:** divide by number of teams. Simple, predictable, wrong incentive. The team publishing ten events a day pays the same as the team publishing ten million.
- **Split by usage:** meter consumption, charge proportionally. Harder to build, best incentive. The cost of a design choice lands on the team that made it.
- **Absorb centrally:** the platform team eats it. Cleanest for consumers, worst for accountability. Free at the point of use gets used wastefully.

The article argues usage-based allocation earns its implementation cost for any shared service expensive enough to matter, because it's the only one of the three that changes behavior. This tool shows you exactly how much the other two cost you in misaligned incentives.

---

## What's in the workbook

Four tabs:

### 1. Start Here
Orientation: the three methods, the three tabs, and the honest limits.

### 2. Chargeback Allocator
The main tab. **Edit only the shaded blue cells:** the total monthly shared cost, the untaggable %, and each team's usage weight (any unit: messages, GB logged, queries run). It computes:

- Each team's usage share.
- Each team's bill under **split equally** and **split by usage**, side by side.
- The **cross-subsidy** per team: how much each team overpays (or underpays) under equal split versus usage.
- The **biggest cross-subsidy** (the most a single light team overpays), the untaggable residual, and the "absorb centrally" case (everyone pays zero, platform eats it all).

### 3. Cross-AZ Example
The article's worked data-transfer example: two chatty services split across availability zones. Set the monthly cross-AZ traffic and the per-GB rate and it shows the monthly and annual cost of the topology choice, plus the saving if you make the hot path zone-local. Defaults reproduce the article's ~$1,000/month.

### 4. Sensitivity
Shows how the cross-subsidy grows as usage skew increases, from even usage (everyone roughly fair) to one whale dominating (light teams overpay heavily under equal split). The more uneven the usage, the more "split equally" taxes everyone else to cover the heavy user.

---

## How to use it

1. Open `shared-services-chargeback-calculator.xlsx` in Excel, Google Sheets, LibreOffice Calc, or Numbers.
2. On **Chargeback Allocator**, set the total shared cost and the untaggable %. Replace the team rows with your own teams and their usage weights.
3. Compare each team's bill under equal vs. usage, and read the cross-subsidy column. That column is the hidden tax of the easy method.
4. Use **Cross-AZ Example** to put a number on a specific topology cost you suspect is hiding in "data transfer."
5. Use **Sensitivity** to see how badly equal split misfires as your usage gets more skewed.

The defaults are illustrative: a $120,000/month shared service across five teams whose usage ranges from a light team (0.5% of usage) to a whale (75%). Under equal split, the light team pays $24,000/month for $600 of actual usage, a $23,400/month cross-subsidy.

---

## The honest limits

- **Precise allocation has a cost.** Don't build per-tenant metering for a $200/month service. Usage-based allocation earns its keep when the shared service is genuinely expensive and the teams are many.
- **Showback before chargeback.** Showing teams their costs without formally billing them is usually the right first step; it changes behavior without the accounting machinery.
- **Defaults are illustrative.** Replace the team rows and the shared cost with your own.

---

## Read the full article

**[Cloud Cost Allocation as Architecture: Your Bill Is an X-Ray](#)** — Engineering Economics, Part 4.
*(Replace this with the published article URL.)*

Part of the Engineering Economics series: why good technical decisions are also financial decisions. This calculator lives in the [engineering-economics-models](../) collection alongside the other models from the series.

---

## License

Released under the [MIT License](../LICENSE). Free to use, copy, and adapt for your own cost-allocation work. Attribution appreciated but not required. No warranty: the numbers are only as good as the assumptions you put in the blue cells.
