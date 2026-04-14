I have IRS Form 990 nonprofit data in a database called PUBLIC_DATA
(loaded from the Snowflake Marketplace - "Snowflake Data: Government Essentials").

The relevant tables in PUBLIC_DATA.PUBLIC_DATA_FREE are:
- IRS_FORM990_INDEX: columns include EIN, BUSINESS_NAME_FULL, STATE, TAX_YEAR, RETURN_TYPE
- IRS_FORM990_TIMESERIES: columns include EIN, TAX_YEAR, FORM_TYPE, VARIABLE, VALUE

Key notes:
- Join the two tables on EIN and TAX_YEAR
- Filter INDEX to RETURN_TYPE = '990' and TIMESERIES to FORM_TYPE = 'IRS990'
- Key financial variables in TIMESERIES: CYTotalRevenueAmt, CYTotalExpensesAmt,
  TotalAssetsEOYAmt, TotalEmployeeCnt

Please:
1. Create a database NONPROFIT_HOL with schema PUBLIC
2. Build a Dynamic Table NONPROFIT_HOL.PUBLIC.NONPROFIT_STATE_SUMMARY
   that aggregates nonprofit financial metrics by state and tax year, with columns:
   - STATE               (two-letter state code)
   - TAX_YEAR            (the filing tax year)
   - ORG_COUNT           (distinct organizations filing Form 990)
   - TOTAL_REVENUE       (sum of CYTotalRevenueAmt)
   - TOTAL_EXPENSES      (sum of CYTotalExpensesAmt)
   - AVG_REVENUE_PER_ORG (average revenue per organization)
   - TOTAL_ASSETS        (sum of TotalAssetsEOYAmt)
   - TOTAL_EMPLOYEES     (sum of TotalEmployeeCnt)

Include only TAX_YEARs 2019 through 2023.
Use a target lag of 1 DAY and my current warehouse.
Show me the DDL before creating anything.
