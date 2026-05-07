# Prompt Template 06 — dbt Model Stub Generation

**Version:** 1.0  
**Tested On:** Claude.ai (free), ChatGPT (free tier)  
**Use Case:** Generate a dbt model stub + schema.yml from a business requirement  
**Author:** RetailEdge DE Team

---

## Template

```
ROLE:
You are a dbt (data build tool) specialist with expertise in building modular,
well-documented dbt models for Snowflake data warehouses.
You follow the dbt best practices guide and the RetailEdge naming convention.

CONTEXT:
dbt project: retailedge_dbt
Target warehouse: Snowflake
Materialisation default: table (use incremental only if explicitly needed)
Source tables available: orders_fact, customers_dim, products_dim, store_dim,
returns_fact, customer_segments, campaign_attribution, revenue_daily
Naming convention: [domain]_[entity]_[grain] e.g. orders_daily_summary, customers_ltv_monthly

TASK:
Generate a dbt model stub for the following requirement:
[DESCRIBE THE BUSINESS REQUIREMENT / METRIC TO BUILD]

OUTPUT: Provide THREE files:

FILE 1 — models/[suggested_path]/[model_name].sql
The dbt SQL model. Use {{ ref() }} for all source references.
Add a model-level docstring at the top as a SQL comment.
Use CTEs for each logical step.

FILE 2 — models/[suggested_path]/schema.yml
The dbt schema YAML with:
- model name and description
- columns list with description and tests for each column
- Include at minimum: not_null and unique tests on the primary key

FILE 3 — A plain English summary:
- What this model does (2 sentences)
- Suggested owner team
- Recommended refresh schedule
- One potential data quality risk to monitor

CONSTRAINTS:
- Do not use SELECT * in the model
- Add dbt_utils.surrogate_key() for composite primary keys
- Mark slowly-changing columns with a comment if applicable
- Keep the model focused — one model, one grain
```

---

## Example Requirement

"Build a monthly model showing total revenue, order count, and average order value 
per customer segment, for use in the executive retention dashboard."

**Expected model name:** `customers_segment_revenue_monthly`  
**Expected grain:** one row per segment per month

---

## Notes
- Always review the generated {{ ref() }} calls — verify source table names are correct
- The schema.yml tests are suggestions — add domain-specific tests based on your knowledge of the data
- Run `dbt compile` to validate syntax before `dbt run`
- For incremental models, add `unique_key` and `is_incremental()` conditions — ask the model to include these by adding "materialise as incremental" to the task description
