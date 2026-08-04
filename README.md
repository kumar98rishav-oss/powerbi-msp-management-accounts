# MSP Management Accounts — Power BI Finance Dashboard

A management-accounts and financial-analytics dashboard for a **Managed Service Provider (MSP)** — the kind of business that runs outsourced **NOC / SOC / Service Desk** operations. Built in **Power BI** using the source-control-friendly **PBIP / TMDL** format.

> ⚠️ **Sample data.** All figures are **synthetic**, generated purely for demonstration. No real company data is included.

---

## 📊 What it does
It unifies the three things an MSP finance team cares about into one governed **star-schema** model:

- **Billing / resource hours** → utilisation and delivery cost
- **Profit & Loss** → revenue, cost of delivery, overheads, EBITDA, net profit
- **Balance sheet** → cash, receivables, working capital, DSO

…and turns them into a board-ready set of six report pages — every figure reconciling back to one audited revenue total (~£40M across 36 months of sample data).

## 🧩 Data model (star schema)
**Fact tables:** `fct_pnl` (P&L), `fct_Billing` (hours by client × service × month), `fct_bs` (quarterly balance sheet), `fct_target` (budget)
**Dimensions:** `dim_Client`, `dim_service`, `dim_date`, `dim_PnLCategory`

Single-direction relationships, a conformed date dimension, and no fact-to-fact joins.

## 📑 Report pages
1. **Executive Summary** — KPI cards, revenue-vs-target trend, utilisation gauge, revenue mix
2. **P&L / Management Accounts** — common-size P&L matrix + a revenue-to-profit waterfall
3. **Profitability & Margin** — margin by service vs target, profitability quadrant
4. **Client Profitability** — client table, concentration analysis, drill-through
5. **Utilisation** — utilisation by service, Key Influencers, decomposition tree
6. **Balance Sheet & Cash** — cash, AR, deferred revenue, working capital, DSO

## 🧮 DAX highlights
- **Revenue allocation** — where per-client / per-service revenue isn't directly available, the audited P&L revenue is allocated by each account's **share of billable value**, and cost by its **share of actual delivery cost** — so margins vary realistically, yet every slice still reconciles to the audited total.
- **Semi-additive balance sheet** — cash / receivables read at the latest **quarter-end** (closing balance), never summed across periods.
- **Sign-convention P&L** — gross profit and EBITDA derived from a signed P&L (costs stored negative), so subtotals are simple sums.
- **Common-size P&L** — every line expressed as a % of revenue.
- **Time intelligence** — YoY, MoM, fiscal YTD, rolling 12-month (LTM), and a 3-month moving average.

## ▶️ How to run
1. Clone this repo.
2. Place the CSV source files in a folder, and set the **`pFolder`** parameter to that folder path.
3. Open **`MSP Management Accounts.pbip`** in Power BI Desktop (Dec 2023 or later).

Expected source files: `income_statement_wide.csv`, `resource_billing_2023/2024/2025.csv`, `balance_sheet_quarterly_wide.csv`, `clients.csv`, `service_lines.csv`, `targets_long.csv`, `fx_rates.csv`, `chart_of_accounts.csv`.

*(The synthetic CSVs are not committed to keep the repo focused on the model and report definition.)*

## 🛠️ Built with
Power BI Desktop · PBIP project format · TMDL semantic model · DAX · Power Query (M)

## 👤 Author
**Rishav Kumar** — Power BI Developer / Data Analyst · Microsoft **PL-300** certified.
