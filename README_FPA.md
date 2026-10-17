# NovaTech FP&A: Budget vs Actual Variance Dashboard

An interactive Power BI dashboard comparing budget and actual performance for a fictional manufacturing company, **NovaTech Manufacturing Pvt. Ltd.**, with variance analysis on revenue, costs and net profit.

> **Dataset note:** All data in this project, including the budget figures, is **simulated** and created for portfolio and learning purposes. NovaTech Manufacturing Pvt. Ltd. is a fictional company. No real company data is used.

This is the second project on NovaTech. The first project analyses cost structure and profitability; this one compares performance against plan.

---

## Project Overview

The dashboard shows how a finance team would review monthly and full-year performance against budget: where results are on or off plan, and what is driving the gap.

**Business questions it answers:**
- How do actual revenue, costs and net profit compare with budget?
- Is the gap driven by selling more or fewer units (volume) or by selling at a different price?
- Which products, regions, cost types and departments are above or below plan?
- How does budgeted net profit bridge to actual net profit?

---

## Dashboard Pages

| Page | What it shows |
|---|---|
| **1. Executive Variance Summary** | Actual and budget revenue, revenue variance, actual net profit and net profit variance; monthly revenue actual vs budget with variance %; a **net profit bridge** (waterfall) from budget to actual; quarterly variance table; an auto-generated key insight |
| **2. Revenue Variance** | Revenue variance by product, split into **price variance** and **volume variance**; variance by region; price vs volume chart by product |
| **3. Cost Variance** | Total cost and operating expense variance; variance by cost type (material, labour, overheads, operating expenses); monthly cost variance; operating expense variance by department |

**Sign convention:** every variance is shown as **Favourable (+) / Unfavourable (−)**. Revenue and profit above budget are favourable. Costs below budget are favourable. Red and green colouring follows this rule throughout.

### Screenshots

![Page 1: Executive Variance Summary](screenshots/page1-executive-variance-summary.png)
![Page 2: Revenue Variance](screenshots/page2-revenue-variance.png)
![Page 3: Cost Variance](screenshots/page3-cost-variance.png)

---

## Data Model

A star schema with six fact tables and four dimension tables, covering 12 months of 2025 data. Budget tables have the same grain as the actual tables so they can be compared directly.

| Table | Type | Columns |
|---|---|---|
| Sales | Actual fact | Date, Product, Region, Quantity, Revenue |
| Costs | Actual fact | Date, Product, Material Cost, Labour Cost, Overhead |
| Expenses | Actual fact | Date, Department, Expense Category, Amount |
| BudgetSales | Budget fact | Date, Product, Region, Quantity, Revenue |
| BudgetCosts | Budget fact | Date, Product, Material Cost, Labour Cost, Overhead |
| BudgetExpenses | Budget fact | Date, Department, Expense Category, Amount |
| Product | Dimension | Product ID, Product Name, Product Category, Budget Unit Price |
| Date | Dimension | Date, Month, MonthNo, Quarter, Year |
| Region | Dimension | Region |
| Department | Dimension | Department |

**Relationships:** `Date` connects to all six fact tables; `Product` connects to Sales, Costs, BudgetSales and BudgetCosts; `Region` connects to Sales and BudgetSales; `Department` connects to Expenses and BudgetExpenses.

---

## Key DAX Measures

- **Actual vs budget:** Actual and Budget measures for Revenue, Quantity, Material, Labour, Overhead, Direct Cost, Operating Expenses, Total Cost and Net Profit
- **Variance (₹ and %):** Revenue, Material, Labour, Overhead, Operating Expense, Total Cost and Net Profit variance, all on a favourable-positive basis
- **Price and volume variance:** revenue variance split using budget unit price, where Price Variance + Volume Variance = Revenue Variance
- **YTD:** Actual, Budget and Variance year-to-date using `TOTALYTD`
- **Profit bridge:** a disconnected Bridge table with a `SWITCH` measure drives the waterfall chart from Budget Net Profit through each variance driver
- **Cost type table:** a disconnected Cost Type table drives the variance-by-type chart
- **Insight text:** a DAX text measure that writes the key insight from the current filters
- **Display labels:** text measures that format values as ₹ Cr / ₹ L

---

## Sample Findings (Simulated Data)

- Total revenue is almost exactly on budget (about −0.1%), but this hides opposite movements by product: NovaGrid Panel is about 5% above budget while TerraCore Motor is about 5% below.
- Net profit is about 3.6% behind budget, mainly because operating expenses are about 4.6% over budget.
- Sales and Administration are the departments with the largest operating expense overruns in rupee terms.

---

## Limitations and Next Steps

- Cost variances compare actual cost with the **original** budget, so part of any cost variance is simply volume. A **flexed budget** (budget restated at actual volume) would separate volume effects from true cost efficiency.
- Other possible extensions: rolling forecast, scenario analysis, and department-level budget owners.

---

## Tools Used

- Power BI Desktop (data modeling, DAX, report design)
- Microsoft Excel (source dataset)

## Skills Demonstrated

FP&A · Budget vs actual analysis · Variance analysis (price, volume, cost) · Profit bridge · DAX · Data modeling (star schema) · KPI reporting · Dashboard design · Data storytelling

---

## Files in This Repository

| File | Description |
|---|---|
| `NovaTech_FP_A.pbix` | The Power BI report |
| `NovaTech_FPA_Dataset_2025.xlsx` | Simulated source data (actual and budget tables) |
| `screenshots/` | Images of each dashboard page |

## How to Open

1. Install **Power BI Desktop** (free, Windows) from Microsoft.
2. Download `NovaTech_FP_A.pbix` from this repository.
3. Open it in Power BI Desktop. If asked, point the data source to the Excel file you downloaded (Home → Transform data → Data source settings).

---

## Author

**Neethu S**: B.Com graduate and CMA (USA)
[LinkedIn](https://linkedin.com/in/neethu-s-20a787370)
