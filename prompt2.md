I have a Dynamic Table called MEDICARE_HOL.PUBLIC.MEDICARE_SPECIALTY_SUMMARY with columns
for provider specialty, state, provider count, total services, average Medicare payment,
and average beneficiary count.

I want business users to ask natural language questions about this data. Please do three things:

1. Create a semantic view on top of MEDICARE_SPECIALTY_SUMMARY in MEDICARE_HOL.PUBLIC
   - Give dimensions and metrics clear, business-friendly labels
   - Add a description to each field explaining what it means
   - Include at least 5 verified query representations (example questions with expected SQL)
   - Show me the semantic view YAML before creating it

2. Write production-quality system instructions for a Cortex Agent named MEDICARE_AGENT
   using this layered structure:
   - Identity & Scope: name the agent, define its role and business outcome for Finance
     and clinical operations staff
   - User Context: the users are Finance analysts, clinical operations managers, and
     healthcare administrators who interact through a chat UI
   - Domain Background: Medicare Part B payment data — provider-level payments by specialty
     and state; data is aggregated and refreshed hourly
   - Style: concise responses, prefer charts when data can be visualized, professional tone
   - Safeguards: decline questions it cannot answer accurately; do not attempt to calculate
     rates or projections not in the data; handle empty results gracefully
   - Orchestration: for all data questions use the Cortex Analyst tool backed by the
     semantic view; parallelize tool calls where possible
   - Response Instructions: define "current" as the most recent data available; hide tool
     names from users; if no results are found, say so clearly rather than guessing

3. Give me the step-by-step instructions to create the agent in Snowsight (AI & ML > Agents),
   paste in the system instructions, and add the semantic view as a Cortex Analyst tool

Suggest 5 natural language questions to test the agent after setup.
