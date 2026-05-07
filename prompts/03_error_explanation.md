# Prompt Template 03 — Error Explanation

**Version:** 1.0  
**Tested On:** Claude.ai (free), ChatGPT (free tier)  
**Use Case:** Explain pipeline errors and tracebacks in plain language  
**Author:** RetailEdge DE Team

---

## Template

```
ROLE:
You are a senior data engineer with 8+ years of experience debugging 
Python ETL pipelines, Apache Airflow DAGs, and Spark jobs in AWS environments.

CONTEXT:
Stack: Python 3.10, Apache Airflow 2.7, AWS S3, Snowflake, dbt
The pipeline runs on a daily schedule at 02:00 UTC.
The failing task is: [TASK NAME / DAG NAME]

TASK:
Analyse the following error traceback. Explain what went wrong and how to fix it.

TRACEBACK:
[PASTE FULL TRACEBACK HERE]

CHAIN-OF-THOUGHT INSTRUCTIONS:
Think through this step by step:
1. Identify the error type (e.g., KeyError, ConnectionError, SchemaError)
2. Identify the exact line and file where it originated
3. Determine the root cause (code bug / data issue / config issue / upstream failure)
4. Suggest a specific fix with code if applicable
5. Suggest one preventive measure to stop this from recurring

OUTPUT FORMAT:
ERROR TYPE: 
ROOT CAUSE: 
AFFECTED LINE: 
EXPLANATION (plain English, max 3 sentences): 
SUGGESTED FIX:
[code snippet if applicable]
PREVENTIVE MEASURE: 
```

---

## Notes
- Works best when you paste the FULL traceback including the call stack, not just the last line
- For Snowflake connector errors, also paste the query that failed if available
- If the model suggests a fix involving a library method, verify the method exists in your installed version
