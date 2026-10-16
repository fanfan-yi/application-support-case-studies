# Case Study 05 — Oracle EBS PO Auto-Approval Business Controls

## Overview

This case study describes an enhancement to an existing Oracle E-Business Suite (EBS) Purchase Order auto-approval process.

The existing procurement process used Oracle standard Global Blanket Purchase Agreement (GBPA) functionality to source requisitions and create Standard Purchase Orders.

A previously customised program then evaluated eligible Incomplete Standard POs and initiated the Oracle PO Approval Workflow when the PO referenced a valid GBPA and passed the existing price validation.

The Procurement team requested additional business controls to prevent specific purchasing scenarios from being automatically approved without buyer review.

My responsibility was to analyse the requirements with Procurement, define how the controls could be implemented using available Oracle EBS data, and translate the agreed business rules into PL/SQL logic within the existing auto-approval program.

---

## Business Problem

The existing auto-approval process improved purchasing efficiency by allowing eligible GBPA-based Standard POs to proceed through the Oracle PO Approval Workflow automatically.

However, Procurement identified several scenarios where buyer review was still required:

1. Urgent requisitions should be reviewed and prioritised by a buyer rather than processed through normal background auto-approval.
2. Purchases exceeding category-specific amount thresholds should require buyer review.
3. Potential duplicate purchases within a short period should be reviewed before approval.

The objective was not to replace the existing auto-approval process, but to introduce additional controls so that automation would continue only when the PO met the agreed business rules.

---

## Existing Process

The process consisted of two separate stages.

### Oracle Standard Functionality

Oracle EBS standard GBPA sourcing functionality was used in the requisition-to-purchase-order process.

Eligible requisitions were sourced against GBPAs and converted into Standard Purchase Orders.

### Existing Customisation

An existing PL/SQL package, originally implemented by an Oracle consultant, processed Incomplete Standard POs.

The program checked whether the PO referenced an active and approved GBPA and validated the PO line price against the corresponding agreement price.

When the existing eligibility conditions were satisfied, the program initiated the standard Oracle EBS PO Approval Workflow (`POAPPRV`).

The enhancement described in this case study added additional business controls to this existing process.

---

## My Role

I was responsible for the business-control enhancement rather than the original GBPA sourcing or auto-approval framework.

My responsibilities included:

- Discussing the requested controls with the Procurement team
- Proposing how each business requirement could be translated into system logic
- Refining the rules through discussions with users
- Analysing Oracle EBS PO and requisition data relationships
- Implementing the agreed controls in PL/SQL
- Performing scenario-based developer testing
- Supporting Procurement user validation
- Deploying the enhancement to production

---

## Business Control 1 — Urgent Requisition Review

### Requirement

Urgent requisitions required buyer attention and should not proceed through the normal auto-approval path.

Buyers used their purchasing work process to identify and prioritise these urgent requirements.

### Implementation

The program traced the Standard PO back to its source requisition through the purchasing distribution relationships:

```text
PO_HEADERS_ALL
        ↓
PO_DISTRIBUTIONS_ALL
        ↓
PO_REQ_DISTRIBUTIONS_ALL
        ↓
PO_REQUISITION_LINES_ALL
        ↓
PO_REQUISITION_HEADERS_ALL
```

The requisition line `URGENT_FLAG` was used to determine whether the original requirement had been marked as urgent.

If an urgent source requisition was identified, the PO was excluded from the auto-approval path and remained available for buyer review.

This preserved human intervention for time-sensitive purchasing rather than automatically processing every eligible GBPA-based PO.

---

## Business Control 2 — Purchasing Category Amount Threshold

### Requirement

Procurement required purchases above an agreed category-specific amount threshold to be reviewed by a buyer.

A single fixed threshold was not appropriate because purchasing limits differed by category.

### Implementation

The enhancement evaluated the purchasing category associated with the PO and compared the purchasing amount against the configured category threshold.

The implementation used category configuration stored in Oracle EBS and incorporated the PO exchange rate when evaluating the amount.

Conceptually:

```text
PO Line
   ↓
Purchasing Category
   ↓
Category-specific threshold
   ↓
PO amount / threshold evaluation
   ↓
Eligible → Continue auto-approval checks
Not eligible → Buyer review
```

The logic also considered requisition source information. WIP- and MRP-originated requirements were handled as defined exceptions within the eligibility logic.

This converted the Procurement team's category-based approval policy into a system-enforced control rather than relying only on manual buyer checks.

---

## Business Control 3 — Potential Duplicate Purchase Detection

### Requirement

Procurement wanted to reduce the risk of the same organisational requirement being purchased repeatedly within a short period because of insufficient communication between requesters.

### Implementation

For the PO being evaluated, the program searched other recently created PO lines for the same:

- Item
- Accounting code combination
- Five-day period

The core comparison used:

```text
Same ITEM_ID
        +
Same CODE_COMBINATION_ID
        +
Other PO created within the previous 5 days
```

The Oracle Accounting Flexfield represented by `CODE_COMBINATION_ID` includes cost centre / department information.

It was used as the most granular available accounting identifier for distinguishing organisational purchasing requirements in this control.

The current PO itself was excluded from the comparison.

If another matching purchase was identified, the PO was excluded from auto-approval so that the buyer could review the potential duplicate.

---

## Approval Decision Flow

```text
Oracle Standard GBPA Process
Requisition → Standard PO
              ↓
      Incomplete Standard PO
              ↓
      Urgent Requisition?
          Yes → Buyer Review
              ↓ No
    Category Amount Control
       Does not pass → Buyer Review
              ↓ Pass
Potential Duplicate Purchase?
          Yes → Buyer Review
              ↓ No
 Existing GBPA / Price Validation
              ↓ Pass
      Oracle POAPPRV Workflow
```

The enhancement introduced a business-control layer before the existing auto-approval logic was allowed to initiate the Oracle PO Approval Workflow.

---

## Technical Implementation

The solution involved:

- Oracle E-Business Suite
- Oracle Purchasing / Procurement
- PL/SQL
- Global Blanket Purchase Agreements (GBPA)
- Oracle PO Approval Workflow (`POAPPRV`)
- Purchasing categories
- Oracle Accounting Flexfield
- PO and requisition distribution relationships
- Requisition source and urgent-request attributes

Key Oracle EBS tables involved included:

```text
PO_HEADERS_ALL
PO_LINES_ALL
PO_DISTRIBUTIONS_ALL
PO_REQ_DISTRIBUTIONS_ALL
PO_REQUISITION_HEADERS_ALL
PO_REQUISITION_LINES_ALL
```

The existing approval process initiated the Oracle workflow through the standard PO approval workflow mechanism rather than directly updating the PO approval status.

---

## Testing and Validation

I performed scenario-based developer testing before releasing the enhancement for user validation.

Test scenarios included:

- An urgent requisition
- A purchase below the configured category threshold
- A purchase above the configured category threshold
- A potential duplicate with the same item and accounting combination within five days
- A normal PO that should remain eligible for auto-approval

These scenarios were used to verify both the exception paths and the normal auto-approval path.

After developer testing, the enhancement was provided to Procurement users for validation.

---

## Production Deployment

The enhancement was deployed to production on **23 May 2023**.

The enhanced controls continue to operate within the procurement process, with no user-reported issues identified to date.

No quantitative reduction in duplicate purchases or manual processing time is claimed because reliable production measurements for those outcomes are not available.

---

## Key Skills Demonstrated

- Oracle EBS Procurement support and enhancement
- Business requirement analysis
- Translating business requirements into ERP control logic
- PL/SQL development
- Oracle EBS data-model analysis
- Requisition-to-PO relationship tracing
- Business-rule and exception-path design
- Oracle Accounting Flexfield understanding
- Scenario-based testing
- Procurement user validation
- Production deployment
- Enhancing an existing customisation while preserving standard Oracle workflow behaviour

---

## Confidentiality

This case study is a sanitised representation of production ERP work.

Company-specific identifiers, internal system details, production data, credentials, and proprietary configuration values have been excluded or generalised.

The purpose of this case study is to demonstrate the problem-solving approach, Oracle EBS knowledge, business-rule analysis, and application support skills involved in the enhancement.
