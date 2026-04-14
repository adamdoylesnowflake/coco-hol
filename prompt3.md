I have a Cortex Agent in Snowflake that answers natural language questions about
IRS Form 990 nonprofit financial data. The agent is named NONPROFIT_AGENT.

Please build a Streamlit in Snowflake application called NONPROFIT_INSIGHTS_APP that:

1. Has a clean, professional header with title "Nonprofit Financial Insights"
   and a subtitle explaining what the app does

2. Includes a text input field where users can type a natural language question

3. Calls the Cortex Agent REST API with the user's question and displays the
   response in a formatted output area

4. Shows a sidebar or section with 5 suggested starter questions users can click
   to auto-populate the input:
   - "Which state has the highest total nonprofit revenue in 2023?"
   - "How has the number of nonprofits changed from 2019 to 2023?"
   - "Show me the top 10 states by total nonprofit employees."
   - "Which states have the highest average revenue per organization?"
   - "Compare total assets between California and New York over time."

5. Uses Snowflake brand colors (primary blue #29B5E8, dark background for headers)

Keep the code simple and focused. Create and deploy the Streamlit app directly in Snowflake.

Show me the complete app.py code before deploying so I can review it.
