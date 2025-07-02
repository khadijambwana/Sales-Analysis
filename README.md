# Superstore End-to-End Sales Analysis

![Language](https://img.shields.io/badge/Language-SQL-blue.svg)
![Database](https://img.shields.io/badge/Database-PostgreSQL-336791.svg)
![Visualization](https://img.shields.io/badge/Dashboard-Tableau%20%7C%20Power%20BI-lightgrey.svg)

## 📂 1. Project Overview

This project is a comprehensive analysis of the Superstore dataset, aimed at uncovering data-driven insights to improve business performance. Using PostgreSQL, I explored sales patterns, customer behavior, and product profitability to answer critical business questions and provide actionable recommendations.

---

## ❓ 2. Business Questions

This analysis sought to answer key questions from four perspectives:

*   **Financial Performance:** What are the overall sales and profit margins? How do discounts impact profitability?
*   **Geographic Analysis:** Which regions, states, and cities are the top-performing markets?
*   **Product Analysis:** Which product categories and sub-categories are the most and least profitable? Are there products that sell well but lose money?
*   **Customer & Operations:** Who are our most valuable customers? What are the most efficient shipping methods?

---
## 🛠️ 3. Tech Stack & Tools


*   **Data Cleaning & Exploration:** Microsoft Excel
*   **Database & Analysis:** SQL (PostgreSQL), pgAdmin
*   **Data Visualization & Dashboarding:** Microsoft Power BI


---
v## 🔍 4. Analysis, Findings & Insights

Here are the key findings from the SQL queries performed on the dataset.

### a. Overall Financial Performance
*   **Finding:** The superstore achieved total sales of approximately $2.3 million, yielding a total profit of $287k, resulting in an overall profit margin of **12.45%**. While positive, this indicates room for margin optimization.
    ```sql
    -- Total Sales, Profit, and Overall Profit Margin
    SELECT
        SUM(sales) AS total_sales,
        SUM(profit) AS total_profit,
        ROUND((SUM(profit) / SUM(sales)) * 100, 2) AS total_margin_percentage
    FROM orders;
    ```

### b. The Impact of Discounts
*   **Finding:** Discounts have a severe and direct impact on profitability. While low discounts (1-20%) are manageable, discounts of 21-40% lead to a sharp drop in average profit, and discounts above 40% consistently result in significant losses per order.
    ```sql
    -- Impact of Discount Levels on Profitability
    SELECT
        CASE
            WHEN discount = 0 THEN 'No Discount'
            WHEN discount <= 0.2 THEN 'Low Discount (1-20%)'
            WHEN discount <= 0.4 THEN 'Medium Discount (21-40%)'
            ELSE 'High Discount (40%+)'
        END AS discount_level,
        ROUND(AVG(profit), 2) AS avg_profit,
        COUNT(order_id) AS number_of_orders
    FROM orders
    GROUP BY discount_level
    ORDER BY discount_level;
    ```

### c. Product Profitability Insights
*   **Finding:** The **Technology** category is the primary driver of both sales and profit. Conversely, **Furniture**, particularly 'Tables' and 'Bookcases', generates high sales but suffers from substantial losses, making them critical areas for re-evaluation.
    ```sql
    -- Identify High-Selling but Low-Profit Products (Margin < 10%)
    SELECT
        p.product_name,
        SUM(sales) AS total_sales,
        SUM(profit) AS total_profit,
        ROUND(SUM(profit)/SUM(sales)*100, 2) AS profit_margin
    FROM orders o
    JOIN products p ON o.product_id = p.product_id
    GROUP BY p.product_name
    HAVING SUM(sales) > 10000 AND (SUM(profit)/SUM(sales)) < 0.1
    ORDER BY profit_margin ASC;
    ```

### d. Geographic & Customer Analysis
*   **Finding:** The **West** region, particularly California and Washington, is the most lucrative market. Our top 10 customers contribute disproportionately to total sales, highlighting an opportunity for a VIP loyalty program.
    ```sql
    -- Top 10 Customers by Total Sales
    SELECT
        c.customer_id,
        c.customer_name,
        SUM(o.sales) AS total_sales
    FROM orders o
    JOIN customers c ON o.customer_id = c.customer_id
    GROUP BY c.customer_id, c.customer_name
    ORDER BY total_sales DESC
    LIMIT 10;
    ```
## 🗂️ 5. SQL Queries

For a detailed look at the technical analysis, the complete set of SQL queries used for this project can be found in the file below.

**[➡️ View the Complete SQL Query Log](sql_queries.md)**
---

## 5. 📊 Interactive Dashboard

For a visual and interactive summary of these findings, please view the dashboard created to complement this analysis. The dashboard allows for dynamic filtering by region, category, and date.

[➡️ View the Dashboard screenshot Here]
(sales_dashboard.png)

---

## 🏆 6. Key Achievements

*   **Identified Major Profit Drivers & Loss Leaders:** Pinpointed 'Technology' as the most profitable category and identified 'Tables' and 'Bookcases' as significant loss-making products, providing clear targets for strategic intervention.
*   **Quantified Discount Impact:** Demonstrated with data that high discounts directly correlate with financial losses, providing a strong case for revising the company's discount strategy.
*   **Located Key Markets:** Identified top-performing geographic regions and cities, enabling focused marketing campaigns and optimized inventory allocation.
*   **Demonstrated Advanced SQL Proficiency:** Utilized a range of SQL techniques including complex joins, aggregations, CTEs (Common Table Expressions), and conditional logic (`CASE` statements) to extract meaningful insights from raw data.

---

## 📬 7. Contact Me

I am actively seeking opportunities in Data Analytics. If you would like to discuss this project or other potential collaborations, please feel free to reach out.

*  👤**Name:** [Khadija Mbwana]
* 🔗 **LinkedIn:** [www.linkedin.com/in/khadija-mbwana]
*  📧 **Email:** [mbwanakhadija77@gmail.com]
