# SAP-MM-Purchase-Order-Risk-Monitoring
In SAP MM, standard Purchase Order reports provide transactional data such as vendor, material, quantity, and value. However, they do not evaluate procurement risk.

In real business scenarios, procurement teams must identify:
- High-value purchase orders
- Critical material procurement
- Orders that require additional review or approval

Without automated risk evaluation, this analysis is manual, error-prone,
and inconsistent across users.

---
## Solution Overview

This project implements a **risk-aware Purchase Order monitoring solution**
using SAP ABAP.

The solution:
- Retrieves Purchase Order data from SAP MM tables
- Evaluates procurement risk using extensible business rules
- Presents actionable insights in an analytical ALV report

Business logic is **decoupled from reporting logic**, allowing risk rules to be
modified without changing the report.

---

## Key Features

- MM-based analytical report for Purchase Orders
- Dynamic risk classification (LOW / MEDIUM / HIGH)
- Human-readable risk reason for transparency
- Enhancement-based business rule implementation
- Clean SALV ALV output with business-friendly labels

---

## Technical Design

### Architecture

SAP MM Tables
(EKKO, EKPO, LFA1, MARA)
        |
        v
Enhancement Logic
(Function Module)
        |
        v
Analytical Report
(SALV ALV)

---

### Components

#### 1. ABAP Report
**ZMM_PO_RISK_REPORT**

Responsibilities:
- Data selection and joins
- Calling enhancement logic
- Displaying results using SALV ALV

No business rules are implemented in the report.

---

#### 2. Enhancement Logic
**Z_MM_PO_RISK_EVALUATE (Function Module)**

Responsibilities:
- Evaluate Purchase Order risk
- Apply business rules such as:
  - High PO value
  - Critical material category
- Return risk level and reason to the report

This logic is reusable and can be extended without modifying the report.

---

#### 3. DDIC Structure
**ZMM_PO_RISK_OUT**

- Unified output structure
- Shared between report and enhancement
- Ensures loose coupling and consistency

---

## Why This Is an Enhancement-Based Design

Although implemented using a function module, this solution follows SAP
enhancement principles:

- Business rules are isolated from the report
- No standard SAP objects are modified
- Logic is reusable across reports or future processes
- Changes in business rules do not require report changes

This design aligns with SAP best practices for extensibility and maintainability.

---

## Tables Used (SAP MM)

- EKKO – Purchase Order Header
- EKPO – Purchase Order Item
- LFA1 – Vendor Master
- MARA – Material Master

---

## Use Case

Procurement analysts can use this report to:
- Identify risky purchase orders instantly
- Focus on high-impact procurement decisions
- Reduce manual review effort
- Support audit and compliance processes

---

## Notes

- Developed and tested in a sandbox/training SAP system
- Data availability may vary based on system setup

---

## Author

SAP ABAP | MM Analytics | Enhancement-Based Design
