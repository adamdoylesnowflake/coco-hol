I have the CMS Medicare Part B Provider Utilization and Payment Data loaded from the Snowflake Marketplace into a database called MEDICARE_HOL. 

Please help me:
1. Explore the tables in MEDICARE_HOL to understand the schema and key columns
2. Build a Dynamic Table called MEDICARE_SPECIALTY_SUMMARY in MEDICARE_HOL.PUBLIC that aggregates the data by provider specialty and state

The Dynamic Table should contain:
- PROVIDER_SPECIALTY: cleaned provider specialty description
- PROVIDER_STATE: two-letter state abbreviation
- PROVIDER_COUNT: number of distinct providers in that specialty/state
- TOTAL_SERVICES: total number of services billed
- AVG_MEDICARE_PAYMENT: average Medicare allowed payment amount
- AVG_BENEFICIARY_COUNT: average number of unique Medicare beneficiaries per provider

Use a target lag of 1 HOUR and my current warehouse.

Show me the DDL before creating anything so I can review it.
