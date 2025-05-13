# -Analyzing-Motorcycle-Part-Sales
# Wholesale Revenue Analysis by Product Line

## Overview

This project analyzes wholesale sales data from a motorcycle parts company that operates three warehouses (North, Central, West). The company sells various product lines and accepts multiple payment methods (Credit Card, Cash, Bank Transfer), each incurring a different transaction fee.

The goal is to compute the **net revenue** per product line, grouped by **month** and **warehouse**, filtering only **Wholesale** transactions.

## Dataset Description

The analysis is based on a single table: `sales`, which contains the following columns:

| Column        | Type    | Description                                           |
|---------------|---------|-------------------------------------------------------|
| order_number  | VARCHAR | Unique identifier for each order                     |
| date          | DATE    | Date of the order (June to August 2021)              |
| warehouse     | VARCHAR | Warehouse from which the order was made              |
| client_type   | VARCHAR | Type of client: 'Retail' or 'Wholesale'              |
| product_line  | VARCHAR | Product category of the order                         |
| quantity      | INT     | Number of units ordered                               |
| unit_price    | FLOAT   | Price per product unit                                |
| total         | FLOAT   | Total value of the order                              |
| payment       | VARCHAR | Payment method used (Credit Card, Transfer, Cash)     |
| payment_fee   | FLOAT   | Percentage fee charged based on the payment method    |

## Objective

Calculate the **net revenue** per `product_line`, `month`, and `warehouse` for all **Wholesale** transactions.  
Net revenue is computed as:


## Output Format

| product_line   | month   | warehouse | net_revenue |
|----------------|---------|-----------|-------------|
| Braking System | June    | Central   | 12345.67    |
| Engine Parts   | July    | West      | 9876.54     |
| ...            | ...     | ...       | ...         |

The results are sorted by:
1. `product_line`
2. `month`
3. `net_revenue` in descending order

## SQL Query

```sql
SELECT
    product_line,
    TO_CHAR(date, 'Month') AS month,
    warehouse,
    ROUND(SUM(total) - SUM(total * payment_fee / 100), 2) AS net_revenue
FROM sales
WHERE client_type = 'Wholesale'
GROUP BY product_line, TO_CHAR(date, 'Month'), warehouse
ORDER BY product_line,
         TO_CHAR(date, 'Month'),
         net_revenue DESC;
This project is for internal analytics purposes only. All rights reserved by the motorcycle parts company.

---

Let me know if you'd like a version with Markdown badges, links to the database file, or integration with Jupyter/Colab.
