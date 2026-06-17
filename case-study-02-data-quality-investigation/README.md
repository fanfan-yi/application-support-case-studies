# Case Study 02 - Approval Date Data Quality Investigation

## Issue

While analysing procurement approval lead times, I was unable to calculate the difference between creation_date and approved_date due to date conversion errors.

Error message:

Failed to parse timestamp value.

---

## Environment

* Procurement Data (Excel)
* Google Drive
* Google Sheets
* SQL Analysis

---

## Investigation

Steps performed:

1. Reviewed the date conversion logic.
2. Examined approval_date sample records.
3. Compared date formats across multiple purchase orders.
4. Validated source data consistency.
5. Identified records causing parsing failures.

---

## Findings

Multiple date formats were stored in the same column.

Examples:

Format A

05/14/2026 14:24:41

Format B

2026/5/4 下午 06:16:26

The inconsistent formats prevented successful date conversion and lead-time calculations.

---

## Root Cause

The approval_date field contained inconsistent date formats entered or generated through different processes.

The lack of a standard date format caused data quality issues during analysis.

---

## Resolution

Identified the affected records and proposed data standardisation before performing lead-time calculations.

Data cleansing should be completed before future reporting activities.

---

## Lessons Learned

* Data quality validation should be performed before analysis.
* Date format consistency is critical for reporting accuracy.
* Investigation should begin with source data validation rather than assuming SQL logic is incorrect.
* Root cause analysis helps prevent recurring reporting issues.

---

## Skills Demonstrated

* Data Quality Investigation
* Root Cause Analysis
* Reporting Analysis
* Data Validation
* Problem Solving
* Documentation
