# 📊 Superstore Sales Analysis (SQL + Power BI)

## 📌 Project Overview
This project analyzes the **Superstore dataset (9,994 rows)** using **SQL** for data transformation and **Power BI** for visualization.  
The objective is to uncover insights about sales, profit, customers, seasonal patterns, and regional performance to support data-driven decision-making.  

**Tools Used:**  
- MySQL (Data Cleaning & Analysis)  
- Power BI (Visualization & Dashboards)  
- GitHub (Version Control & Documentation)  

---

## ⚡ SQL Analysis

### 1. Top Performing Products
```sql
SELECT `Product Name`, 
       SUM(`Profit`) AS total_profit,
       ROUND(SUM(`Profit`)/SUM(`Sales`) * 100, 2) AS profit_margin_pct
FROM superstore
GROUP BY `Product Name`
ORDER BY total_profit DESC
LIMIT 10;
```
**Insight:**
1. Printers and accessories generate the highest profits.
2. Some furniture items have negative margins due to discounts.

## 2. Regional Performance
```sql
SELECT `Region`,
       COUNT(*) AS total_orders,
       ROUND(SUM(`Sales`), 2) AS total_sales,
       ROUND(SUM(`Profit`), 2) AS total_profit,
       ROUND(SUM(`Profit`)/SUM(`Sales`) * 100, 2) AS profit_margin_pct
FROM superstore
GROUP BY `Region`
ORDER BY total_profit DESC;
```
**Insight:**
1. The West region contributes the most profit.
2. The South region has lower margins compared to others.

### 3. Seasonal Trends
```sql
SELECT YEAR(`Order Date`) AS order_year,
       MONTH(`Order Date`) AS order_month,
       ROUND(SUM(`Sales`), 2) AS monthly_sales,
       ROUND(SUM(`Profit`), 2) AS monthly_profit
FROM superstore
GROUP BY order_year, order_month
ORDER BY order_year, order_month;
```
**Insight:**
1. Sales peak during November–December (holiday season).
2. Profitability fluctuates, suggesting discount-heavy months.

### 4. High-Value Customers
```sql
WITH customer_metrics AS (
    SELECT `Customer ID`,
           `Customer Name`,
           COUNT(*) AS total_orders,
           SUM(`Sales`) AS lifetime_sales,
           SUM(`Profit`) AS lifetime_profit,
           ROUND(AVG(`Sales`), 2) AS avg_order_value
    FROM superstore
    GROUP BY `Customer ID`, `Customer Name`
)
SELECT `Customer Name`,
       total_orders,
       ROUND(lifetime_sales, 2) AS lifetime_sales,
       ROUND(lifetime_profit, 2) AS lifetime_profit,
       avg_order_value
FROM customer_metrics
ORDER BY lifetime_profit DESC
LIMIT 10;
```
**Insight:**
1. A small group of customers drive a large share of profits.
2. High-value customers tend to purchase technology items.s.

### 5. Category Performance
```sql
SELECT `Customer Name`, SUM(`Profit`) AS total_profit
FROM superstore
GROUP BY `Customer Name`
ORDER BY total_profit DESC
LIMIT 5;
```
**Insight:**
1. Technology leads in both sales and profit.
2. Furniture has inconsistent profitability due to high discounts.
