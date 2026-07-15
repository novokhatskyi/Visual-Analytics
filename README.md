# Visual Analytics — Power BI Projects

Data-analytics portfolio built during the GoIT Data Analytics course.
Each folder is a self-contained Power BI project covering the full workflow:
data cleaning in Power Query, a star-schema model with DAX measures, and an
interactive multi-page dashboard that answers clear business questions and
states its own limitations honestly.

---

## Projects

### 📊 [sales-dashboard-powerbi](./sales-dashboard-powerbi) · Online Retail

Five-page sales-performance dashboard on an online-retail dataset
(Jan–Aug 2024, 240 transactions). Dark themed, with cross-page synced slicers,
report-page tooltips and a Decomposition Tree.

The heart of the project is the **data-cleaning work** — the raw data was
intentionally dirty and required recovering corrupted units from
`Revenue / Price`, fixing an impossible 222% tax rate, filling tax gaps by
time period, and normalising products that appeared under two categories,
several of which were discovered *through the dashboard itself*.

**Key insight — revenue ≠ volume.** Electronics drives **44% of revenue** with
only **13% of units** (avg. price ≈ $517); Clothing is the opposite (28% of
units, 10% of revenue). Optimising by "units sold" would point to the wrong
products. The report also states its limitations honestly: in this synthetic
data Region and Category are near-collinear, so the regional view is an artifact
of data generation rather than customer behaviour.

📄 Full write-up: [project README](./sales-dashboard-powerbi/README.md)

**Tools:** Power BI · Power Query (M) · DAX · pandas · Excel

---

### 🚲 [bike-shop-sales-dashboard](./bike-shop-sales-dashboard) · Bike Retailer

Six-page sales-analytics dashboard on a multi-country bike retailer
(33.5K orders, Jan 2023 – Jun 2024). Turns raw transactional data into business
insights across sales trends, products, geography, clients and AI-driven analysis.

**Key insight — revenue ≠ profit.** The Bikes category generates ~50% of revenue
($10.8M) at a **negative gross margin (−2.5%)**; profit is actually driven by
accessories (Cleaners 49% margin, Bottles & Cages 31%). The business was
loss-making in early 2023, reached break-even in Q3 2023, and grew to
~$1M gross profit/quarter by Q2 2024. Germany, with 2.5× less revenue than the
US, delivers **higher absolute profit** thanks to a 21.3% margin (vs. 7.5% US).

**Highlights:** star schema + DAX Calendar, measures incl.
`Orders Count = DISTINCTCOUNT(Order_ID)` and `Profit Margin %`; drillable
Category → Sub-Category matrix, country → state map, and AI visuals
(Decomposition Tree, Key Influencers).

📄 Full write-up: [project README](./bike-shop-sales-dashboard/README.md)

**Tools:** Power BI · Power Query · DAX

---

## Common approach across both projects

- **Data cleaning first** — profiling messy data (floating-point noise in
  quantities, corrupted values, inconsistent categories) and fixing it in
  Power Query, with decisions documented rather than hidden.
- **Sound modelling** — star schema with a dedicated DAX Calendar dimension,
  marked as a date table, month names sorted by month number.
- **Reusable measures** — base aggregations composed into derived metrics
  (margin %, AOV, distinct order counts).
- **Report design** — one page = one business question, consistent navigation
  and filter panels on every page, AI visuals for free-form exploration.

**Author:** Oleksandr Novokhatskyi
