# engineering-economics-models

**Working spreadsheet models for the Engineering Economics series: live formulas, sensitivity analysis, yours to use.**

Each article in the [Engineering Economics](https://the-architect-ds.medium.com/list/engineering-economics-3b3a950758c7) series makes an argument about the money behind a technical decision. The models in this repo let you run that argument against your own numbers instead of just reading mine.

Every workbook follows the same conventions:

- **Edit only the shaded blue cells.** Everything else is a formula.
- **Defaults reproduce the worked example** from the matching article, so you can see the model working before you replace the numbers.
- **The honest limits are stated on a "Start Here" tab.** These price cost, not value, and the output is only as good as the assumptions you put in.

---

## Models

### [`build-buy-automate-tco/`](./build-buy-automate-tco/) — Build vs. Buy vs. Automate TCO calculator

A five-year total-cost-of-ownership model for the build-vs-buy-vs-automate decision. The build estimate is the deposit; maintenance is the mortgage. Simple cash mode plus an advanced after-tax NPV mode (capex vs. opex, Section 174 amortization, the tax shield, discounting).

Companion to **"Build vs. Buy vs. Automate: The Real TCO Nobody Models"** (Part 5).

> Download: [`build-buy-automate-tco-calculator.xlsx`](./build-buy-automate-tco/build-buy-automate-tco-calculator.xlsx)

### [`migration-crossover/`](./migration-crossover/) — Migration crossover calculator

Finds the crossover year when keeping an aging system stops being cheaper than replacing it. Plots cumulative "keep" vs. "replace" over time, folds in the hidden costs of not migrating, and sweeps the maintenance growth rate you're least sure of. Sunk cost is deliberately absent from the model.

Companion to **"The Economics of Migration: Sunk Cost vs. Rip-and-Replace"** (Part 6).

> Download: [`migration-crossover-calculator.xlsx`](./migration-crossover/migration-crossover-calculator.xlsx)

---

## How to use any of them

1. Open the `.xlsx` in Excel, Google Sheets, LibreOffice Calc, or Numbers.
2. Read the **Start Here** tab first.
3. Edit the blue input cells on the main calculator tab with your own numbers.
4. Read the results, then check the **Sensitivity** tab to see whether your answer survives being wrong about the assumption you're least sure of.

Each model's own `README.md` has the full tab-by-tab walkthrough.

---

## The series

Part of **Engineering Economics: Why Good Technical Decisions Are Also Financial Decisions**. The full list of published articles lives [here](https://the-architect-ds.medium.com/list/engineering-economics-3b3a950758c7).

---

## License

Released under the [MIT License](./LICENSE). Free to use, copy, and adapt for your own decisions. Attribution appreciated but not required. No warranty: the numbers are only as good as the assumptions you put in the blue cells.
