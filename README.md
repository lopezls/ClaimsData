# Healthcare Claims Data Cleaning & Validation Pipeline
## Overview

This project simulates a common real-world data operations task: taking a messy, multi-source healthcare claims export and turning it into a clean, validated, audit-ready dataset ready for reporting and analysis. *The dataset uses synthetic data for practice purposes, this contains no real patient information*. However, this project was done to as an exercise to reflect the kinds of data quality issues that show up in real client-submitted healthcare data such as: inconsistent formatting, missing values, and duplicate records.

## What This Project Does
- Cleans and standardizes a raw healthcare claims dataset (60+ records) with realistic data quality issues
- Documents the reasoning behind each cleaning decision, not just the mechanics
- Joins the cleaned claims data against a provider reference table
- Produces a summary report broken down by claim status and provider specialty
## Data Quality Issues Addressed
|Issue| Solution |	Why|
| ----------- | ----------- | ----------- |
|Duplicate Rows (5 rows) |	Removed |	Prevents double-counting in summary statistics |
|Mixed date formats (2025-05-21, 01/16/2025, 14-Jul-2025)|Standardized to a single datetime type using pd.to_datetime(format="mixed") |	Enables consistent date-based sorting/filtering |
|Inconsistent casing & whitespace in claim_status (Paid, PAID, denied )|	Stripped and lowercased |	Ensures identical statuses aren't treated as different categories |
|Missing diagnosis_code (4 rows)|	Filled with "Unknown"|	Preserves the rest of the claim's valid data rather than discarding the  entire row|
|Missing claim_amount (5 rows)|	Flagged with a new amount_missing column and left as null	|Avoids creating a false claim amount of $0.00 and allows pandas automatically excludes nulls from .sum()/.mean()|
|Missing provider_id (17 rows)|	Filled with "Unknown"|	Preserves claim data rather than dropping usable records|

## Key Design Decision: Left Join, Not Inner Join

When joining the cleaned claims data against the provider reference table, I used a left join on provider_id. An inner join would have dropped these claims from the dataset entirely. Preserving these claims is essential to understanding the entire picture of claims and billing activity, regardless of whether provider information is provided or not.

##  Results Summary
- **60 usable claims** after removing duplicates
- **Total claim amount:** $128,445.95 (average: $2,335.38, across the 55 claims with a recorded amount)
- **By claim status:** 36 paid ($81,667.96), 7 pending ($8,157.94), 12 denied ($38,620.05)
- **By specialty:** Primary Care generated the most claims revenue ($53,309.87), followed by Endocrinology ($23,350.25) and Cardiology ($19,897.09)

## Tools Used

Python, Pandas, Jupyter Notebook

## Files
- **DataClaims.ipynb** — full cleaning, joining, and analysis pipeline with documented reasoning
- **messy_claims_data.csv** — the raw (synthetic) claims dataset
- **provider_lookup.csv** — provider reference table used in the join

## Note

Once again this dataset contains simulated data for practice purposes and does not contain any real patient information. It was built to mirror common real-world healthcare data quality issues for skill demonstration.
