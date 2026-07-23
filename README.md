# E-commerce-Sales-Dashboard
Interactive 5-page Power BI dashboard analyzing e-commerce sales, profitability, and representative performance - built with a full star schema and 25+ DAX measures.

---

Project Overview
==================

The **E-commerce Sales Dashboard** is a 5-page interactive Power BI report built to track and analyze sales performance, regional revenue, sales representative rankings, and customer/channel behaviour for a retail sales dataset.

The dashboard is designed to support data-driven decision-making by presenting KPIs, trend analysis, and profitability breakdowns in a clean, navigable, light-themed interface.

---

Dashboard Pages
====================

| # | Page | Description |
|---|---|---|
| 1 | **Index** | Landing page with report title, page navigation cards, and key business insights |
| 2 | **Executive Summary** | Headline KPIs (Total Sales, Total Profit, Profit Margin %, Total Transactions), sales trend vs prior year, category mix, regional sales, monthly sales vs. target |
| 3 | **Sales & Profitability** | Sales performance by representative, profit margin by category, price-volume relationship, region × category matrix, category sales trend by quarter, slicers for region/date/category |
| 4 | **Customer & Channel Behaviour** | Sales by customer segment, channel performance by segment, payment method distribution, discount rate vs. target, sales driver decomposition tree |
| 5 | **Sales Representative's Performance & Rankings** | Representatives leaderboard (sales, profit, rank), 30-day rolling sales trend, total sales by representatives, monthly sales trajectory, representative selector buttons, date range slicer |

---
Data Model
====================

The report uses a **star schema** with the following tables:

**Fact Table:**
- `Fact_Sales` — Sale_Date, Product_ID, RegionID, SalesRepID, CategoryID, CustomerTypeID, PaymentMethodID, SalesChannelID, Sales_Amount, Quantity_Sold, Unit_Cost, Unit_Price, Discount

**Dimension Tables:**
- `Dim_Date` - Date, Year, Quarter, MonthNum, MonthName, MonthShort, YearMonth, Day, WeekdayName, WeekdayNum, IsWeekend, WeekOfYear
- `Dim_Region` - RegionID, Region
- `Dim_SalesRep` - SalesRepID, Sales_Rep
- `Dim_ProductCategory` - CategoryID, Product_Category
- `Dim_CustomerType` - CustomerTypeID, Customer_Type
- `Dim_PaymentMethod` - PaymentMethodID, Payment_Method
- `Dim_SalesChannel` - SalesChannelID, Sales_Channel

**Calculated Table:**
- `Measures` - empty shell table used purely to organize all DAX measures in one place in the Fields pane

All dimension tables connect to `Fact_Sales` via single-direction, one-to-many relationships on their respective ID columns. `Dim_Date` is marked as the official Date Table.

---

Tools & Technologies
====================

- **Power BI Desktop**
- **DAX** - Calculated measures for KPIs, time intelligence, ranking, and contribution analysis
- **Power Query (M)** - Data cleaning, column splitting into dimensions, ID merging, type correction
- **Model View Relationships** - Star schema with single-direction one-to-many joins
- **Sort by Column** - Correct chronological ordering for Month Short / Quarter fields
- **Sync Slicers** - Region, Date, and Category filters synced across pages
- **Decomposition Tree** - Exploratory visuals
- **Page Navigation** — Button-based navigation from the Index page

---

DAX Measures Used
====================

| Measure | Description |
|---|---|
| `Total Sales` | Sum of Sales_Amount |
| `Total Quantity` | Sum of Quantity_Sold |
| `Total Transactions` | Count of rows in Fact_Sales |
| `Total Cost` | Sales_Amount scaled by Unit_Cost ÷ Unit_Price ratio |
| `Total Revenue (Price x Qty)` | Unit_Price × Quantity_Sold, summed |
| `Total Profit` | Total Sales − Total Cost |
| `Profit Margin %` | Total Profit ÷ Total Revenue |
| `Avg Discount %` | Average of Discount |
| `Discount Impact` | Sales_Amount × Discount, summed |
| `Avg Sale Value` | Total Sales ÷ Total Transactions |
| `Avg Unit Price` | Average of Unit_Price |
| `Avg Quantity per Order` | Total Quantity ÷ Total Transactions |
| `Avg Profit per Transaction` | Total Profit ÷ Total Transactions |
| `Sales PY` | Total Sales, same period last year |
| `Sales MoM %` | Month-over-month sales growth |
| `Sales YTD` / `Sales QTD` | Year-to-date / quarter-to-date sales |
| `Sales YoY %` | Year-over-year sales growth |
| `Rolling 30-Day Sales` | Trailing 30-day sales total |
| `Sales Rank by Rep / Category / Region` | Rank via RANKX, ignoring current filters |
| `Top Category Flag` | Flags the #1 ranked category |
| `% of Total Sales` / `% of Total Sales by Category` | Contribution to grand total |
| `New vs Returning Sales Split` | Share of sales from new customers |
| `Distinct Sales Reps / Products Sold / Active Days` | Distinct count measures |

---

Key Features
====================

- **Star Schema Data Model** - 1 fact table + 7 dimension tables for fast, scalable filtering
- **25 DAX Measures** - organized under a dedicated `Measures` table, covering totals, profitability, time intelligence, ranking, and contribution
- **Light Theme Design** - off-white canvas, white cards, deep slate blue + soft teal accents, muted category palette, consistent across all pages
- **Index / Landing Page** - page navigation buttons and a Key Insights panel, shown before any analytical page
- **Synced Slicers** - Region, Date range, and Category filters apply across multiple pages at once
- **Decomposition Tree** - click-to-explore sales breakdown by Region → Channel → Customer Type
- **30-Day Rolling Trend** - smooths daily sales noise to reveal real rep-level trends
- **Correct Chronological Sorting** - Month Short and Quarter fields sorted by their numeric order columns, not alphabetically
- **Icon-Based KPI Cards** - light-palette icon badges for Total Sales, Total Profit, Profit Margin %, Total Transactions

---

Key Business Insights
====================

- **Alice outperforms her sales rank** - placing 4th in sales but 2nd in profit, showing that sales volume alone doesn't reflect true performance.
- **David is the strongest overall performer** - leading both sales and profit, with a notable sales spike in late 2023 worth investigating.
- **North is the best-performing region** - consistently leading across regional sales and customer segments.
- **Sales are evenly distributed across all four product categories** - with no single category dominating revenue.
- **Growth is flat** - current sales closely match the prior year, and the current month is meeting, not exceeding, its target.

---

Dataset Details
====================

| Table | Approx. Rows | Key Fields |
|---|---|---|
| `Fact_Sales` | 1,000 transactions | Sale_Date, Sales_Amount, Quantity_Sold, Unit_Cost, Unit_Price, Discount |
| `Dim_Region` | 4 | North, South, East, West |
| `Dim_SalesRep` | 5 | Alice, Bob, Charlie, David, Eve |
| `Dim_ProductCategory` | 4 | Clothing, Electronics, Food, Furniture |
| `Dim_CustomerType` | 2 | New, Returning |
| `Dim_PaymentMethod` | 3 | Cash, Credit Card, Bank Transfer |
| `Dim_SalesChannel` | 2 | Online, Retail |
| `Dim_Date` | 730 days | Full calendar, 2023–2024 |

---

How to Use
====================

1. Download the `.pbix` file.
2. Open it in **Power BI Desktop** (free download from Microsoft).
3. On the **Index** page, click any navigation card to jump to that section of the report.
4. Use the **slicers** (Region, Date range, Category) on each analytical page to filter the visuals — synced slicers will carry your selection across pages.
5. Hover over any chart for detailed tooltips; click into the **Decomposition Tree** or **Q&A box** on the Customer & Channel Behaviour page to explore data interactively.
6. On the Sales Representative's Performance page, click a rep's name button to filter the whole page to that individual.
