# Prompt Template 02 — Schema Documentation

**Version:** 1.0  
**Tested On:** Claude.ai (free), ChatGPT (free tier)  
**Use Case:** Auto-generate clear table documentation for the data catalogue  
**Author:** RetailEdge DE Team

---

## Template

```
ROLE:
You are a technical documentation specialist embedded in a data engineering team.
You write clear, accurate, and useful table documentation for data catalogues 
used by both engineers and non-technical business analysts.

CONTEXT:
Company: RetailEdge Analytics (fashion retail, India)
Catalogue platform: Confluence wiki
Audience: Mix of data engineers, business analysts, and product managers

TASK:
Write a complete data catalogue entry for the following table.
Use ONLY the information provided — do not invent fields or relationships.

TABLE INFORMATION:
Table Name: [TABLE NAME]
Raw Schema (paste CREATE TABLE or column list here): 
[PASTE SCHEMA HERE]
Sample rows (optional):
[PASTE 3-5 SAMPLE ROWS HERE IF AVAILABLE]

CONSTRAINTS:
- Do not invent column descriptions — if purpose is unclear, write "Purpose unclear — verify with pipeline owner"
- Do not assume relationships unless foreign key is explicit in the schema
- Keep descriptions readable by a non-technical analyst

OUTPUT FORMAT:
Return the documentation in this exact structure:

## Table: [table_name]
**Domain:** [infer from table name/columns]
**Owner:** [write "Unknown — assign during catalogue review"]
**Update Frequency:** [infer if possible, else "Unknown"]
**Contains PII:** [Yes/No — check for email, phone, name, address columns]
**Source System:** [infer if possible, else "Unknown"]
**Row Granularity:** [one row per ___]

### Description
[2-3 sentence plain English description of what this table contains and its primary use]

### Column Reference
| Column Name | Data Type | Description | Nullable | Notes |
|-------------|-----------|-------------|----------|-------|
[one row per column]

### Known Issues / Warnings
[List any data quality concerns visible from schema or sample rows. If none, write "None documented."]

### Common Use Cases
[2-3 bullet points of typical analyst queries that use this table]
```

---

## Notes
- Run on one table at a time for best quality
- After generation, have the pipeline owner review and correct the "Owner" and "Source System" fields
- Commit the output as a .md file to the catalogue GitHub repo
