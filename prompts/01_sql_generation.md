# Prompt Template 01 — SQL Generation

**Version:** 1.0  
**Tested On:** Claude.ai (free), ChatGPT (free tier)  
**Use Case:** Generate accurate, optimised SQL for analyst data requests  
**Author:** RetailEdge DE Team

---

## Template

```
ROLE:
You are a senior data analyst with deep expertise in Snowflake SQL. You write clean, 
efficient, well-commented SQL that follows best practices for large-scale data warehouses.

CONTEXT:
Database: Snowflake
Primary tables available: orders_fact, customers_dim, products_dim, store_dim, 
revenue_daily, returns_fact, customer_segments
All monetary values are in INR. Timestamps are in UTC.
orders_fact contains one row per completed order with columns: 
order_id, customer_id, product_id, store_id, order_date, total_amount, 
payment_method, status, quantity

TASK:
Write a Snowflake SQL query to answer the following business question:
[INSERT BUSINESS QUESTION HERE]

CONSTRAINTS:
- Avoid SELECT * — only select columns needed to answer the question
- Use CTEs instead of nested subqueries for readability
- Add a brief comment above each CTE explaining its purpose
- Filter large tables early (before joins) to reduce scan cost
- If the question involves aggregation, include a GROUP BY and relevant ORDER BY
- Do not use LIMIT unless the question specifically asks for top-N results

OUTPUT FORMAT:
Return only the SQL query with inline comments. 
Then add a 2-line plain English explanation of what the query does.
Do not add any other text.
```

---

## Example Usage

**Input question:** "Show me total revenue by city for March 2025, only for completed orders"

**Expected output structure:**
```sql
-- Step 1: Filter orders to the relevant period and status
WITH filtered_orders AS (
    SELECT 
        o.order_id,
        o.store_id,
        o.total_amount
    FROM orders_fact o
    WHERE o.order_date BETWEEN '2025-03-01' AND '2025-03-31'
      AND o.status = 'completed'
),
-- Step 2: Join with store dimension to get city
orders_with_city AS (
    SELECT 
        f.total_amount,
        s.city
    FROM filtered_orders f
    JOIN store_dim s ON f.store_id = s.store_id
)
-- Step 3: Aggregate revenue by city
SELECT 
    city,
    SUM(total_amount) AS total_revenue,
    COUNT(*) AS order_count
FROM orders_with_city
GROUP BY city
ORDER BY total_revenue DESC;
```
*This query calculates total completed order revenue per city in March 2025. 
It uses early filtering before the join to minimise the data scanned.*

---

## Notes
- Always validate output SQL by checking column names against the actual schema before running
- For time-series questions, use DATE_TRUNC() for consistent period grouping
- Hallucination risk: LLMs sometimes invent column names — verify against data dictionary
