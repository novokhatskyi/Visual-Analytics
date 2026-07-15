# Bike Shop Sales Dashboard (Power BI)

Interactive sales analytics dashboard built in Power BI Desktop as part of the GoIT Data Analytics course. The report analyzes 33.5K orders from a multi-country bike retailer (January 2023 – June 2024) and turns raw transactional data into business insights.

## 📊 Report Structure

The report contains 6 pages, each answering a specific business question:

| Page | Business Question |
|------|-------------------|
| **Home** | Landing page: key KPIs, global filters, and navigation to all report sections |
| **Sales Trends** | How do revenue and profit change over time? (monthly/quarterly dynamics) |
| **Products** | What sells and what actually earns? (revenue vs. margin by category) |
| **Geography** | Where do we sell? (countries, states, interactive map) |
| **Clients** | Who buys? (age groups, gender distribution) |
| **Analysis** | AI-driven exploration: what drives revenue and profitability? |

<!-- Додай сюди скріншоти: -->
![Home page](screenshots/home.png)
![Sales Trends](screenshots/sales-trends.png)
![Products](screenshots/products.png)
![Geography](screenshots/geography.png)
![Clients](screenshots/clients.png)
![Analysis](screenshots/analysis.png)

## 🔍 Key Insights

- **Revenue ≠ profit.** The Bikes category generates ~50% of total revenue ($10.8M) while operating at a **negative gross margin (−2.5%)**. Profit is actually driven by accessories: Cleaners (49% margin), Bottles and Cages (31%), Caps (31%).
- **The business turned around in mid-2023.** The first two quarters of 2023 were loss-making; the company reached break-even in Q3 2023 and grew gross profit to ~$1M/quarter by Q2 2024 — while revenue was rising the whole time.
- **Germany is the most efficient market.** With 2.5× less revenue than the US, Germany delivers a higher absolute gross profit ($871K vs. $762K) thanks to a 21.3% margin (vs. 7.5% in the US).
- **Age matters, gender doesn't.** The core audience is 20–49 years old; within every age group, male and female purchasing behavior is nearly identical.

## 🛠 Technical Implementation

**Data preparation (Power Query):**
- Fixed floating-point noise in the Quantity column (values like 2.9998 → 3) by enforcing whole-number types
- Removed 33 rows (~0.1%) with unidentifiable sub-category values
- Applied Fixed Decimal type to all monetary columns to avoid accumulation errors

**Data model:**
- Star schema: fact table (34.8K rows) + dedicated Calendar dimension table
- Calendar built with DAX (`CALENDAR(MIN/MAX)`), marked as a date table, with Year / Quarter / Month columns and correct custom sorting (Month Name sorted by Month Number)

**DAX measures:**
- `Total Revenue`, `Total Cost`, `Total Gross Profit`, `Total Quantity` — base aggregations
- `Profit Margin % = DIVIDE([Total Gross Profit], [Total Revenue])`
- `Orders Count = DISTINCTCOUNT(Order_ID)` — counts unique orders, not line items

**Report features:**
- Navigation panel (page buttons) and filter panel (slicers) on every page
- Report-level date filter to exclude the incomplete last month
- Conditional formatting: profit columns colored by sign (loss = red)
- Age binning into custom groups (<30, 30–39, 40–49, 50–59, 60+)
- Drillable matrix (Category → Sub-Category) and map with country → state drill-down
- AI visuals: **Decomposition Tree** (flexible root-cause exploration of revenue) and **Key Influencers** (statistical drivers of profitability)

## 🚀 How to View

1. Download the `.pbix` file
2. Open with [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
3. All data is embedded — no external connections required

*Dataset: synthetic training data provided by the GoIT Data Analytics course.*
