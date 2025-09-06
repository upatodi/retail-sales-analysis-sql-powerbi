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
**Insight:**
Printers and accessories generate the highest profits.
Some furniture items have negative margins due to discounts.
