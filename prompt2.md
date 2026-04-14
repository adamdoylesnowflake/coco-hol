I have a Dynamic Table: NONPROFIT_HOL.PUBLIC.NONPROFIT_STATE_SUMMARY
with columns for state, tax_year, org_count, total_revenue, total_expenses,
avg_revenue_per_org, total_assets, and total_employees.

Please do three things:

1. Create a semantic view on top of NONPROFIT_STATE_SUMMARY in NONPROFIT_HOL.PUBLIC
   - Give dimensions and metrics clear, business-friendly labels
   - Add a description to each field explaining what it means
   - Include at least 5 verified query representations (example questions with expected SQL)
   - Show me the semantic view YAML before creating it

2. Write production-quality system instructions for a Cortex Agent named NONPROFIT_AGENT
   using this layered structure:
   - Identity & Scope: name the agent, define its role and business outcome for
     nonprofit sector analysis and grant-making strategy
   - User Context: the users are foundation analysts, policy researchers, and nonprofit
     sector professionals who interact through a chat UI
   - Domain Background: IRS Form 990 data — annual financial returns filed by US nonprofits;
     data covers revenue, expenses, assets, and employees aggregated by state and tax year
     from 2019 to 2023
   - Style: concise responses, prefer charts when data can be visualized, professional tone
   - Safeguards: decline questions it cannot answer accurately; do not attempt to calculate
     projections not in the data; handle empty results gracefully
   - Orchestration: for all data questions use the Cortex Analyst tool backed by the
     semantic view; parallelize tool calls where possible
   - Response Instructions: define "current" as the most recent tax year available; hide
     tool names from users; if no results are found, say so clearly rather than guessing

3. Give me the step-by-step instructions to create the agent in Snowsight (AI & ML > Agents),
   paste in the system instructions, and add the semantic view as a Cortex Analyst tool

Suggest 5 natural language questions to test the agent after setup.
