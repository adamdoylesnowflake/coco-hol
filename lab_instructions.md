# Cortex Code Hands-On Lab
## Building Nonprofit Financial Insights with Cortex Code
**Duration**: 90 minutes | **Platform**: Snowflake Snowsight | **Industry**: Nonprofit / Public Sector (IRS Form 990)

---

## What You'll Build

In this lab you will use Cortex Code — Snowflake's AI coding agent — to build a complete nonprofit analytics solution in three steps, using only natural language prompts:

| Part | What You Build | Time |
|---|---|---|
| **1** | A Dynamic Table aggregating IRS Form 990 nonprofit financial data | ~25 min |
| **2** | A Snowflake Intelligence Agent that answers NL questions about the data | ~25 min |
| **3** | A Streamlit app providing a polished UI for the agent | ~25 min |

You will write **three prompts**. Cortex Code does the rest.

---

## Setup (~10 minutes)

### Step 1: Add the Government Essentials Data from the Marketplace

1. In Snowsight, click **Data** in the left nav → **Marketplace**
2. Search for: `Snowflake Public Data (Free)`
3. Click the listing and click **Get**
4. When prompted for a database name, leave the default: `PUBLIC_DATA`
5. Accept the terms and click **Get Data**

> The dataset is free and contains public IRS Form 990 data — annual financial returns filed by every US nonprofit organization.

### Step 2: Create a Workspace

1. In Snowsight, click **Projects** in the left nav → **Worksheets**
2. Click **+** → **Worksheet** to open a new SQL worksheet
3. Set the **role** to your current user role and **warehouse** to your available warehouse

### Step 3: Open Cortex Code

1. Click the **blue star icon** (✦) in the bottom-right corner of Snowsight
2. Cortex Code opens as a side panel
3. It automatically connects using your current role and warehouse

> You are ready. Everything from here is done by pasting a prompt and reviewing what Cortex Code proposes.

---

## Part 1: Build a Dynamic Table (~25 minutes)

**The story**: IRS Form 990 contains raw nonprofit financial filings from over 350,000 organizations per year. Your strategy team needs a clean, always-refreshing aggregated summary by state and tax year so leadership can track nonprofit sector health and funding patterns without running expensive queries on the raw data.

### Instructions

1. Open the **Cortex Code** panel (blue star, bottom-right)
2. Copy the **Part 1 Prompt** from `prompts.md` (or the prompt card in your deck) and paste it into the Cortex Code input
3. Press **Enter**
4. Cortex Code will:
   - Discover the Form 990 tables and columns in `PUBLIC_DATA.PUBLIC_DATA_FREE`
   - Propose a Dynamic Table definition
   - Ask for your approval before creating anything
5. Review the proposed SQL. When satisfied, approve each step
6. Verify the table was created:

```sql
SHOW DYNAMIC TABLES LIKE 'NONPROFIT_STATE_SUMMARY%';
SELECT * FROM NONPROFIT_HOL.PUBLIC.NONPROFIT_STATE_SUMMARY LIMIT 10;
```

### Expected Output
A Dynamic Table named `NONPROFIT_STATE_SUMMARY` in database `NONPROFIT_HOL` with columns including:
- `STATE` — two-letter state code
- `TAX_YEAR` — filing tax year (2019–2023)
- `ORG_COUNT` — number of distinct nonprofits filing Form 990
- `TOTAL_REVENUE` — total revenue across all organizations in that state/year
- `TOTAL_EXPENSES` — total expenses across all organizations
- `AVG_REVENUE_PER_ORG` — average revenue per organization
- `TOTAL_ASSETS` — total assets at end of year
- `TOTAL_EMPLOYEES` — total employees across all organizations

---

## Part 2: Create a Snowflake Intelligence Agent (~25 minutes)

**The story**: The Dynamic Table is live and refreshing, but business users can't write SQL. You need a natural language interface so stakeholders can ask questions like *"Which state has the most nonprofit revenue?"* without touching code.

### Why agent instructions matter

A Cortex Agent without system instructions gives generic, inconsistent answers. Good instructions define who the agent is, who it serves, what it can and cannot do, and how it should behave when results are empty or a question is out of scope. The prompt for this part asks Cortex Code to generate production-quality instructions using a seven-layer framework:

| Layer | What it covers |
|---|---|
| Identity & Scope | Agent name, role, business outcome |
| User Context | Who the users are and how they interact |
| Domain Background | IRS Form 990 data context and terminology |
| Style & Tone | Conciseness, chart preference, professional tone |
| Safeguards | What the agent must decline or handle carefully |
| Orchestration | Which tool to call for which question type |
| Response Instructions | Temporal rules, empty-result handling, tool name hiding |

### Instructions

1. Keep the **Cortex Code** panel open
2. Copy the **Part 2 Prompt** from `prompts.md` and paste it in
3. Press **Enter**
4. Cortex Code will produce three things:
   - A semantic view on `NONPROFIT_STATE_SUMMARY` with business-friendly labels and verified query examples
   - A complete set of layered agent system instructions ready to paste into Snowsight
   - Step-by-step instructions for wiring the agent in the UI
5. Review the semantic view YAML and approve it
6. Copy the generated agent instructions — you will paste them in the next step
7. Follow Cortex Code's instructions to create the Agent in Snowsight:
   - Navigate to **AI & ML** → **Agents** in the left nav
   - Click **+ Agent**
   - Name it `NONPROFIT_AGENT`
   - Paste the generated system instructions into the **Instructions** field
   - Under **Tools**, add the semantic view as a **Cortex Analyst** tool
   - Click **Create**
8. Test your agent in the Agent chat window:

> *"Which state has the highest total nonprofit revenue?"*
> *"How has the number of nonprofits in California changed from 2019 to 2023?"*
> *"Show me the top 5 states by total nonprofit employees."*
> *"What happens if I ask about something not in the data?"* (tests safeguards)

### Expected Output
- A semantic view named `NONPROFIT_STATE_SV` (or similar) in `NONPROFIT_HOL.PUBLIC`
- A Cortex Agent with production-quality system instructions governing its behavior
- A working agent in Snowsight that answers data questions accurately and declines gracefully when it cannot help

---

## Part 3: Build a Streamlit Application (~25 minutes)

**The story**: Leadership loves the agent, but wants a branded, shareable interface they can bookmark — not a raw chat window. You need a polished Streamlit app deployed inside Snowflake.

### Instructions

1. Keep the **Cortex Code** panel open
2. Copy the **Part 3 Prompt** from `prompts.md` and paste it in
3. Press **Enter**
4. Cortex Code will:
   - Generate a complete Streamlit in Snowflake application
   - Include a nonprofit-themed UI with a text input, response display, and suggested questions
   - Create the app file and deploy it
5. When Cortex Code asks for approval, review the app code and approve
6. Open the deployed app:
   - Navigate to **Projects** → **Streamlit** in the left nav
   - Click your new app to open it
7. Test it by entering a question in the text box

### Expected Output
A deployed Streamlit app named `NONPROFIT_INSIGHTS_APP` (or similar) featuring:
- A Snowflake-branded header with a nonprofit analytics subtitle
- A text input field for natural language questions
- A response area displaying the agent's answer
- A sidebar or section with 5 suggested starter questions

---

## Wrap Up

You've built a complete nonprofit analytics solution in 90 minutes using three natural language prompts:

1. **Raw Marketplace data** → Governed Dynamic Table (always fresh)
2. **Dynamic Table** → Cortex Agent with semantic understanding
3. **Cortex Agent** → Polished Streamlit app for business users

### Clean Up (Optional)
If you want to remove the objects created during this lab:

```sql
DROP DATABASE IF EXISTS NONPROFIT_HOL;
-- Remove the Streamlit app via Projects > Streamlit > your app > Delete
-- Remove the Agent via AI & ML > Agents > NONPROFIT_AGENT > Delete
```

---

## Tips & Troubleshooting

| Issue | Resolution |
|---|---|
| Cortex Code can't find the Government Essentials data | Make sure `GOVERNMENT__ESSENTIALS` was created in setup; try saying *"search my Snowflake account for IRS Form 990 tables"* |
| Dynamic Table shows 0 rows | The lag may not have fired yet — run `ALTER DYNAMIC TABLE NONPROFIT_HOL.PUBLIC.NONPROFIT_STATE_SUMMARY REFRESH` |
| Agent gives no results | Verify the semantic view is valid; ask Cortex Code *"audit my semantic view for issues"* |
| Streamlit app shows an error | Ask Cortex Code *"fix the error in my Streamlit app"* and paste in the error message |
| Running low on credits | Switch to a simpler follow-up prompt; avoid re-running large tasks |

---

## Reference: Credit Usage

This lab is designed to run within **5 Cortex Code credits** per participant.

| Part | Est. Interactions | Est. Credits |
|---|---|---|
| Setup | 0 | 0 |
| Part 1 | 4–8 | ~0.15–0.25 |
| Part 2 | 5–8 | ~0.15–0.25 |
| Part 3 | 5–10 | ~0.15–0.30 |
| **Total** | **14–26** | **~0.45–0.80** |

Remaining buffer: ~4.2–4.6 credits for iteration and exploration.
