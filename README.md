# RetailEdge DE Prompt Library

A versioned library of reusable prompt templates for data engineering workflows, 
built during the GenAI for Data Engineers pilot (Week 1, April 2025).

---

## What This Is

Prompt engineering templates that standardise how the RetailEdge data engineering 
team uses LLMs. Each template is tested on at least two free-tier models and 
committed here as a versioned markdown file.

**Tools tested:** Claude.ai (free), ChatGPT free tier, Llama 3.1 via Hugging Face

---

## Prompt Templates

| # | File | Use Case | Tested Models |
|---|------|----------|---------------|
| 01 | [01_sql_generation.md](prompts/01_sql_generation.md) | Generate Snowflake SQL from business questions | Claude.ai, ChatGPT |
| 02 | [02_schema_documentation.md](prompts/02_schema_documentation.md) | Auto-document tables for data catalogue | Claude.ai, ChatGPT |
| 03 | [03_error_explanation.md](prompts/03_error_explanation.md) | Explain pipeline errors and tracebacks | Claude.ai, ChatGPT |
| 04 | [04_data_quality_rules.md](prompts/04_data_quality_rules.md) | Generate DQ checks (Great Expectations / SQL) | Claude.ai, ChatGPT |
| 05 | [05_pipeline_description.md](prompts/05_pipeline_description.md) | Write Confluence docs from pipeline code | Claude.ai, ChatGPT |
| 06 | [06_dbt_model_stubs.md](prompts/06_dbt_model_stubs.md) | Generate dbt model + schema.yml stubs | Claude.ai, ChatGPT |

---

## How to Use a Template

1. Open the relevant `.md` file
2. Copy the template block (between the triple backticks)
3. Replace all `[PLACEHOLDER]` values with your actual content
4. Paste into Claude.ai or ChatGPT
5. Review the output carefully before using in production

---

## Key Findings from Pilot Testing

- **Structured prompts with ROLE + CONTEXT + OUTPUT FORMAT consistently outperformed free-form prompts** across all three models tested
- Claude.ai free tier produced the most complete outputs with type annotations and edge-case handling
- ChatGPT free tier was faster but hallucinated method names in ~20% of code-generation runs
- Llama 3.1 via Hugging Face required more iterative prompting but produced correct logic when given explicit role prompts

---

## Contributing

To add a new template:
1. Create a new file: `prompts/[NN]_[use_case_name].md`
2. Follow the existing structure: ROLE / CONTEXT / TASK / CONSTRAINTS / OUTPUT FORMAT
3. Test on at least 2 models before committing
4. Update this README table
5. Open a PR for team review

---

## Versioning

- `v1.x` — Initial templates from intern pilot (April 2025)
- Templates are versioned within each file. Breaking changes increment the minor version.

---
