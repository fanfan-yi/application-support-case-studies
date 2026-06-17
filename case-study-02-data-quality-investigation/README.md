# Case Study 02 - Approval Date Data Quality Investigation

## Issue

While analysing procurement approval lead times, the SQL query failed when attempting to calculate the difference between creation_date and approved_date.

Error message:

Failed to parse timestamp value.

---

## Environment

* Oracle ERP Procurement Data
* Google BigQuery
* SQL
* Procurement Reporting Analysis

---

## Investigation

Steps performed:

1. Reviewed the SQL query and timestamp conversion logic.
2. Examined approval_date sample records.
3. Compared date formats across multiple purchase orders.
4. Validated source data consistency.
5. Identified records causing parsing failures.

---

## Findings

* Multiple date formats were stored in the same column.
* Some records used standard timestamp formats.
* Other records contained localised date strings.
* Timestamp conversion functions could not process all records successfully.

Examples:

Format A

05/14/2026 14:24:41

Format B

2026/5/4 下午 06:16:26

---

## Root Cause

The approval_date field contained inconsistent date formats generated from different sources or processes.

The lack of a standardised date format prevented successful timestamp conversion and impacted lead-time calculations.

---

## Resolution

Identified the affected records and proposed a data standardisation approach before performing lead-time analysis.

Analysis activities were temporarily paused until data quality issues could be addressed.

---

## Lessons Learned

* Data quality issues can directly impact reporting accuracy.
* SQL errors are not always caused by query logic.
* Source data validation should be performed before analysis.
* Root cause investigation is essential for reliable reporting.

---

## Skills Demonstrated

* SQL Troubleshooting
* Data Validation
* Root Cause Analysis
* ERP Support
* Reporting Investigation
* Problem Solving
