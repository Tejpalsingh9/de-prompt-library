# Prompt Template 04 — Data Quality Rule Creation

**Version:** 1.0  
**Tested On:** Claude.ai (free), ChatGPT (free tier)  
**Use Case:** Generate Great Expectations or SQL-based DQ checks for a table  
**Author:** RetailEdge DE Team

---

## Template

```
ROLE:
You are a data quality engineer specialising in building validation frameworks
for data warehouses. You write Great Expectations suites and SQL assertion queries.

CONTEXT:
Table: [TABLE NAME]
Platform: Snowflake
Validation framework: Great Expectations (or plain SQL assertions if GE not available)
This table is used for: [DESCRIBE PRIMARY USE — e.g., "daily revenue reporting"]

TABLE SCHEMA:
[PASTE COLUMN LIST WITH TYPES HERE]

SAMPLE DATA (optional):
[PASTE 5 ROWS IF AVAILABLE]

TASK:
Generate a comprehensive set of data quality rules for this table covering:
1. Completeness checks (non-null requirements)
2. Uniqueness checks (primary key / deduplication)
3. Referential integrity checks (foreign key consistency)
4. Value range / domain checks (valid statuses, positive amounts, etc.)
5. Timeliness check (data freshness — latest row should be within 24 hours)

CONSTRAINTS:
- Write each rule as both a plain English description AND a SQL assertion query
- For Great Expectations, also write the expect_* method call
- Mark each rule as CRITICAL (pipeline should fail) or WARNING (log and continue)
- Do not invent business rules — only derive rules that are clearly implied by the schema

OUTPUT FORMAT:
For each rule:
RULE ID: DQ-[TABLE_ABBREV]-[NUMBER]
CATEGORY: [Completeness / Uniqueness / Referential / Domain / Timeliness]
SEVERITY: [CRITICAL / WARNING]
DESCRIPTION: [Plain English]
SQL ASSERTION:
  SELECT COUNT(*) FROM [table] WHERE [condition that should return 0 rows]
GE METHOD: expect_[method_name](column="...", ...)
```

---

## Example

**RULE ID:** DQ-ORD-001  
**CATEGORY:** Completeness  
**SEVERITY:** CRITICAL  
**DESCRIPTION:** order_id must never be null — every row must have a valid order identifier  
**SQL ASSERTION:**
```sql
SELECT COUNT(*) FROM orders_fact WHERE order_id IS NULL;
-- Expected result: 0
```
**GE METHOD:** `expect_column_values_to_not_be_null(column="order_id")`

---

## Notes
- Start with CRITICAL rules before WARNING rules
- Timeliness checks depend on your SLA — adjust the 24-hour threshold as needed
- Run GE suite in a pre-deployment DAG task before any downstream pipelines consume the table
