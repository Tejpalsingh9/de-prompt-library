# Prompt Template 05 — Pipeline Description

**Version:** 1.0  
**Tested On:** Claude.ai (free), ChatGPT (free tier)  
**Use Case:** Auto-generate plain-English documentation for an existing pipeline  
**Author:** RetailEdge DE Team

---

## Template

```
ROLE:
You are a technical writer embedded in a data engineering team.
You translate complex pipeline code into clear documentation for Confluence.

CONTEXT:
Company: RetailEdge Analytics
Audience: New engineers onboarding + business stakeholders
Documentation destination: Confluence wiki page

TASK:
Read the following pipeline code and generate a complete documentation page for it.

PIPELINE CODE:
[PASTE YOUR PYTHON / AIRFLOW DAG / DBT MODEL CODE HERE]

CONSTRAINTS:
- Do not reproduce the code in the documentation — describe what it does in plain English
- Use present tense ("The pipeline reads...", not "The pipeline will read...")
- If you cannot determine a value from the code, write "[TO BE CONFIRMED BY OWNER]"
- Keep the Stakeholder Impact section readable by a non-technical product manager

OUTPUT FORMAT:

## Pipeline: [infer name from code]
**Owner:** [infer from code comments or write TO BE CONFIRMED]  
**Schedule:** [infer from DAG schedule_interval or write TO BE CONFIRMED]  
**SLA:** [TO BE CONFIRMED BY OWNER]  
**Last Updated:** [TO BE CONFIRMED]

### What This Pipeline Does
[3-5 sentence plain English description]

### Source → Destination
| Stage | System | Table/Path | Notes |
|-------|--------|------------|-------|
| Source | | | |
| Intermediate | | | |
| Destination | | | |

### Transformation Steps
[Numbered list of what the pipeline does, in plain English]

### Stakeholder Impact
[Which dashboards or reports depend on this pipeline. Write "Unknown — verify with BI team" if unclear]

### Failure Behaviour
[What happens when this pipeline fails — retry logic, alerts, fallback]

### Known Issues / Technical Debt
[List from code comments or TODOs. Write "None documented." if none found]
```

---

## Notes
- Works well for Airflow DAGs, dbt models, and standalone Python ETL scripts
- After generation, send to the pipeline owner for a 15-minute review before publishing
- Add the Confluence page URL to the pipeline's code as a comment for future reference
