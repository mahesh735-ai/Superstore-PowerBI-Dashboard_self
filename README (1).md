# 📊 E-Commerce Sales Analysis — Power BI Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)

---

## 📌 Project Overview

An interactive 3-page Power BI dashboard analyzing **4 years of e-commerce sales data (2014–2017)** from the Superstore dataset. The goal was to identify revenue drivers, profitability issues, discount impact, and customer behavior to support data-driven business decisions.

---

## 🗂️ Dataset

| Attribute | Details |
|-----------|---------|
| Source | Sample Superstore — Kaggle |
| Time Period | 2014 to 2017 |
| Total Records | ~9,994 orders |
| Tables | Orders, Returns, People |

---

## 🛠️ Tools & Technologies

- **Microsoft Power BI** — Dashboard, DAX measures, data modeling
- **Power Query** — Data cleaning and transformation
- **DAX** — Custom measures and calculated columns
- **Microsoft Excel** — Initial data inspection

---

## 📐 Data Model

Three tables connected in a Star Schema:

```
Orders (Fact Table)
    ├── Returns    [Order ID → Order ID]      Many-to-One
    ├── People     [Region → Region]           Many-to-One
    └── Date Table [Order Date → Date]         Many-to-One
```

---

## 🧹 Data Preprocessing (Power Query)

- Fixed data types: Order Date, Ship Date → Date type
- Postal Code → Text type (to preserve leading zeros)
- Added `Days to Ship` calculated column
- Added `Discount Band` column: No Discount / Low (1-20%) / Medium (21-40%) / High (40%+)
- Verified no null values in key columns: Order ID, Customer ID, Sales, Profit

---

## 📊 Dashboard Pages

### Page 1 — Sales Overview
- KPI Cards: Total Sales ($2.30M), Total Profit ($286.4K), Total Orders (5,009), Profit Margin (12.47%)
- Sales by Segment (Donut), Sales by Region (Bar), Sales by Category (Bar), Monthly Trend (Line)
- Slicers: Year, Region, Category

### Page 2 — Profit Analysis
- KPI Cards: Total Profit, Profit Margin %, Avg Discount, High Discount Orders
- Sales vs Profit by Product (Scatter Plot — annotated)
- Top 5 Profitable Sub-Categories (Bar)
- Discount Impact on Profit (Green→Red gradient bar)

### Page 3 — Customer & Returns
- KPI Cards: Total Customers (793), Return Rate % (5.91%), Top Customer (Sean Miller), Total Returns (296)
- Top 10 Customers by Sales (Horizontal Bar)
- Returns by Category (Bar)
- Top 10 Products by Sales (Horizontal Bar)

---

## 🔑 Key DAX Measures

```dax
Total Sales       = SUM(Orders[Sales])
Total Profit      = SUM(Orders[Profit])
Total Orders      = DISTINCTCOUNT(Orders[Order ID])
Total Customers   = DISTINCTCOUNT(Orders[Customer ID])
Profit Margin %   = DIVIDE([Total Profit], [Total Sales], 0)
Avg Discount      = AVERAGE(Orders[Discount])
Return Rate %     = DIVIDE([Total Returns], [Total Orders], 0)
Sales LY          = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date Table'[Date]))
YoY Growth %      = DIVIDE([Total Sales] - [Sales LY], [Sales LY], 0)
```

---

## 💡 Key Business Insights

1. **Discount = Profit Killer** — Orders with 40%+ discount generate **-0.10M loss**, while no-discount orders yield **+0.32M profit**. Heavy discounting must be reduced on low-margin products.

2. **Technology = Highest Margin** — Technology category leads in both revenue ($0.84M) and profitability. Copiers and Phones are the top sub-categories.

3. **West Region Dominates** — West leads with $0.73M in sales. South ($0.39M) has significant growth potential.

4. **Q4 Seasonal Spike** — November and December show peak sales (0.31M and 0.33M). Inventory and marketing should plan for this seasonal demand.

5. **Consumer Segment = 50%+** — Consumer segment contributes 50.56% of all sales, making it the primary target for growth strategies.

6. **Office Supplies = Highest Returns** — Despite being the lowest-revenue category, Office Supplies has 234 returns — the highest among all categories. Quality or fulfillment issues need review.

---

## 📁 Repository Contents

```
📦 Superstore-PowerBI-Project
 ┣ 📊 Superstore_BI_project_1.pbix        ← Power BI file
 ┣ 📄 Superstore_Project_Documentation.docx ← Full project doc
 ┣ 📄 STAR_Method_Interview_Guide.docx    ← Interview prep
 ┣ 📋 README.md                           ← This file
 ┗ 📂 dataset/
    ┗ Sample_Superstore.xls               ← Raw data
```

---

## 🚀 How to Use

1. Download or clone this repository
2. Open `Superstore_BI_project_1.pbix` in Power BI Desktop
3. If prompted, update the data source path to your local `Sample_Superstore.xls`
4. Explore the 3 dashboard pages with interactive slicers

---

## 🎯 Skills Demonstrated

- Data modeling (Star Schema)
- Power Query data transformation
- DAX measure creation (time intelligence, aggregations, conditional logic)
- Multi-page interactive dashboard design
- Business storytelling through data visualization
- Insight extraction and presentation

---

## 👤 About

**First self-initiated Power BI project** — built completely independently from data loading to final dashboard.

---

*Dataset source: Sample Superstore — available on Kaggle*
