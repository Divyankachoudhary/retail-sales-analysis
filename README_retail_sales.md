# Retail Store Sales Analysis

An end-to-end SQL + Power BI project analyzing retail transaction data to calculate business KPIs, identify customer trends, and surface actionable insights for sales strategy.

---

## 📌 Project Overview

| Detail | Info |
|---|---|
| **Domain** | Retail / E-commerce |
| **Tools** | SQL · Power BI · Power Query · DAX |
| **Dataset** | ~1,000 retail transactions with customer demographics and product categories |
| **Type** | KPI Analysis + Business Insights + Interactive Dashboard |

---

## 🎯 Business Questions Answered

- What is the total revenue, profit, and average transaction value?
- Which product categories generate the most revenue and profit?
- Which customer segments (age group, gender) spend the most?
- When are peak sales hours and peak sales quarters?
- Which categories are underperforming and why?

---

## 🗂 Repository Structure

```
retail-sales-analysis/
│
├── retail.sales sql query.sql       # All SQL queries with comments
├── retail_sales_analysis.pbix       # Power BI dashboard
├── retail_sales_screenshot.png      # Dashboard preview
├── retail_sales.csv                 # Dataset
└── README.md
```

---

## 📋 Dataset Schema

| Column | Description |
|---|---|
| `transaction_id` | Unique ID per sale |
| `sale_date` | Date of transaction |
| `sale_time` | Time of transaction |
| `customer_id` | Unique customer identifier |
| `gender` | Customer gender |
| `age` | Customer age |
| `category` | Product category (Electronics, Clothing, Beauty) |
| `quantity` | Units sold |
| `price_per_unit` | Unit price |
| `cogs` | Cost of goods sold |
| `total_sale` | Total transaction value |

---

## 🗄 SQL Analysis

### KPI Calculations
```sql
-- Total Revenue
SELECT SUM(total_sale) AS total_revenue FROM retail_sales;

-- Total Profit
SELECT SUM(total_sale - cogs) AS total_profit FROM retail_sales;

-- Avg Sale per Customer
SELECT AVG(total_sale) AS avg_sale FROM retail_sales;

-- Unique Customers
SELECT COUNT(DISTINCT customer_id) AS unique_customers FROM retail_sales;
```

### Customer Segmentation
```sql
-- Sales by Age Group
SELECT
  CASE
    WHEN age BETWEEN 18 AND 30 THEN '18-30'
    WHEN age BETWEEN 31 AND 45 THEN '31-45'
    WHEN age BETWEEN 46 AND 60 THEN '46-60'
    ELSE '60+'
  END AS age_group,
  SUM(total_sale) AS total_sales,
  COUNT(*) AS transactions
FROM retail_sales
GROUP BY age_group
ORDER BY total_sales DESC;

-- Sales by Gender
SELECT gender, SUM(total_sale) AS total_sales, ROUND(AVG(total_sale), 2) AS avg_sale
FROM retail_sales
GROUP BY gender;
```

### Category & Profitability Analysis
```sql
-- Category-wise Revenue and Profit
SELECT
  category,
  SUM(total_sale) AS revenue,
  SUM(total_sale - cogs) AS profit,
  ROUND(SUM(total_sale - cogs) / SUM(total_sale) * 100, 2) AS profit_margin_pct
FROM retail_sales
GROUP BY category
ORDER BY revenue DESC;
```

### Time-Based Trends
```sql
-- Peak Sales Hour
SELECT HOUR(sale_time) AS hour, SUM(total_sale) AS revenue
FROM retail_sales
GROUP BY hour
ORDER BY revenue DESC
LIMIT 5;

-- Quarterly Sales Trend
SELECT
  QUARTER(sale_date) AS quarter,
  SUM(total_sale) AS quarterly_revenue
FROM retail_sales
GROUP BY quarter
ORDER BY quarter;
```

---

## 📊 Dashboard Highlights

Built in Power BI with Power Query for data prep and DAX for calculated measures.

- **KPI Cards** — Total Revenue (912K), Total Profit, Unique Customers, Avg Sale per Customer
- **Category Revenue & Profit** — clustered bar chart with profit margin overlay
- **Sales by Age Group** — bar chart showing 46–60 as top segment
- **Gender Split** — donut chart showing female customers spend slightly more
- **Quarterly Trend** — line chart showing Q4 as peak quarter
- **Peak Hours Heatmap** — evening hours (5–8 PM) dominate

---

## 📸 Dashboard Preview

![Retail Sales Dashboard](retail_sales_screenshot.png)

---

## 💡 Key Insights

- **Electronics** generates the highest revenue and profit — priority category for inventory investment
- **The 46–60 age group** is the highest-spending segment — marketing should target this demographic
- **Female customers** have a slightly higher average transaction value than male customers
- **Q4 drives maximum sales** — seasonal promotions in Q4 would have the highest ROI
- **Evening hours (5–8 PM)** are peak sales periods — ideal window for flash sales and push notifications
- **Beauty is the lowest performer** — needs pricing or product-mix review

---

## ⚙️ How to Run

**SQL**
Load `retail_sales.csv` into MySQL / PostgreSQL / SQLite and run the queries in `retail.sales sql query.sql`.

**Power BI**
Open `retail_sales_analysis.pbix` in Power BI Desktop. Update the data source path to point to `retail_sales.csv` if prompted.

---

## 📬 Connect

- 🔗 [LinkedIn](https://www.linkedin.com/in/divyanka-choudhary-64b217259)
- 📁 [My GitHub Portfolio](https://github.com/Divyankachoudhary)

---

*If you found this project useful, consider giving it a ⭐*
