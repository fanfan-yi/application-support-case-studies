# Case Study 01 - Looker Studio Dataset Access Issue

## Issue

While building a procurement dashboard using BigQuery and Looker Studio, the report failed to display data.

Error message:

Dataset access permission error.

---

## Environment

- Google Cloud Platform
- BigQuery
- Looker Studio
- Dataset Location: australia-southeast1

---

## Investigation

Steps performed:

1. Verified BigQuery query execution.
2. Confirmed dataset accessibility.
3. Reviewed IAM permissions.
4. Tested BigQuery views.
5. Reconnected Looker Studio data source.
6. Validated account credentials.

---

## Findings

- BigQuery queries executed successfully.
- Dataset schema was visible in Looker Studio.
- Visualisations could not retrieve dataset records.
- Issue appeared related to dataset access behaviour between Looker Studio and BigQuery.

---

## Workaround

Exported query results and connected the dashboard using Google Sheets to continue dashboard development.

---

## Root Cause Assessment

The issue was not caused by SQL query errors or missing dataset permissions.

Investigation results indicated that:

- BigQuery queries executed successfully.
- Dataset schema was visible in Looker Studio.
- Data retrieval failed when visualisations attempted to access dataset records.

The issue is suspected to be related to the interaction between Looker Studio and the BigQuery dataset configuration.

Further investigation is required to determine the exact root cause.

## Lessons Learned

- Data access issues are not always caused by SQL errors.
- System integration troubleshooting requires validation across multiple layers.
- Temporary workarounds can help maintain project progress while root causes are investigated.

---
## Skills Demonstrated

- Application Support
- System Integration
- Troubleshooting
- Root Cause Analysis
- Reporting Support
- Problem Solving
