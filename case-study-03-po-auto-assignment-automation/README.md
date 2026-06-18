# Case Study 03 - PO Auto Assignment Automation

## Issue

Category-based requisitions required manual assignment by supervisors, creating assignment delays and increasing administrative workload. Supervisors typically reviewed and assigned requisitions in batches rather than immediately after submission.

---

## Environment

* Procurement Data (ERP)
* Oracle ERP R12
* TOAD
* Stored Procedure
* PL/SQL

---

## Investigation

Steps performed:

1. Reviewed the requisition assignment process.
2. Analysed manual and automated assignment volumes to evaluate automation opportunities.
3. Investigated the amount of time supervisors spent assigning buyers.

---

## Findings

The existing process relied on supervisors manually assigning buyers for category-based requisitions.

On a sample day (2026/06/17):

* Total requisitions: 170
* Item-based requisitions: 108
* Category-based requisitions: 45
* Automatically assigned: 39
* Manually assigned: 6

Approximately 86.7% of category-based requisitions could be assigned automatically through predefined business rules.
The findings indicated a significant opportunity to reduce manual effort through process automation.

Manual assignment was mainly required for equipment purchases, maintenance requests and special procurement cases without designated buyers.

---

## Root Cause

The ERP standard functionality only supported automatic assignment for item-based requisitions.

Category-based requisitions depended on supervisor knowledge and manual decision-making, creating delays and increasing administrative workload.

---

## Resolution

Developed a PL/SQL stored procedure to automatically assign buyers based on:

* Company
* Organisation
* Procurement Category

The assignment process was automated through a scheduled job running every five minutes, ensuring timely buyer allocation without supervisor intervention.

Special cases continued to be reviewed manually when required.

---

## Business Impact

* Based on a sample day analysis (2026/06/17), 39 out of 45 category-based requisitions were assigned automatically, achieving an automation rate of approximately 86.7%.
* Reduced the number of category-based requisitions requiring manual assignment from 45 to 6 on the sample day.
* Improved buyer response time by reducing assignment delays.
* Reduced training requirements for new supervisors.
* Standardised buyer assignment rules across procurement processes.

Estimated annual cost saving: Approximately AUD 6,000–9,000, based on an estimated 60 minutes of supervisor effort saved per working day.
The solution also improved procurement cycle responsiveness by reducing waiting time between requisition submission and buyer assignment.

---

## Lessons Learned

* Process automation can deliver measurable operational improvements without major system changes.
* Understanding business rules is as important as technical implementation.
* Automating repetitive tasks allows teams to focus on higher-value activities.
* Close collaboration with procurement stakeholders is critical for successful process improvement.

---

## Skills Demonstrated

* Process Automation
* ERP Support
* PL/SQL Development
* Business Process Improvement
* Stakeholder Collaboration
* Operational Efficiency
* Root Cause Analysis
* Workflow Optimisation
* Business Analysis
* Scheduled Job Automation
