# Master Data Management (MDM) Principles Applied in This Project

## Purpose
This document outlines the MDM principles implemented in both the ADF and Databricks pipelines.  
Both pipelines process Customers, Orders, and Products through RAW → BRONZE → SILVER → GOLD while enforcing identity, quality, and survivorship rules.

---

## Core MDM Principles

### 1. Identity Resolution
Each dataset uses a primary identifier:
- customer_id  
- order_id  
- product_id  

Both pipelines:
- partition by ID  
- apply window functions  
- select the latest record  

Databricks allows more advanced identity logic, but both are compliant.

---

### 2. Deduplication
Both pipelines remove duplicates using window logic.

- **ADF**: rowNumber() over partition  
- **Databricks**: dense_rank(), row_number(), ordering by timestamps  

This ensures only one surviving record per entity.

---

### 3. Survivorship Rules
Survivorship determines which record becomes the “truth.”

Rules applied:
- latest timestamp wins  
- non‑null values preferred  
- consistent attribute selection  

ADF supports basic survivorship.  
Databricks supports full rule sets.

---

### 4. Schema Standardization
Both pipelines enforce:
- consistent column names  
- consistent data types  
- drift handling  
- null normalization  

ADF handles drift automatically.  
Databricks enforces drift through code.

---

### 5. Golden Record Creation
The GOLD layer contains:
- Customer Golden Record  
- Daily Sales Summary  
- Product Performance Model  

Golden records combine:
- deduped attributes  
- validated fields  
- business rules  
- identity‑resolved entities  

Databricks is the preferred tool for this stage.

---

### 6. Auditability & Lineage
- **ADF**: pipeline logs, activity runs  
- **Databricks**: Delta Lake versioning (time travel)  

Both provide traceability, but Databricks offers deeper lineage.

---

## Summary
Both ADF and Databricks pipelines in this project are MDM‑aligned.  
ADF excels at ingestion and schema standardization.  
Databricks excels at identity resolution, dedupe, survivorship, and golden‑record creation.

Together, they demonstrate two valid approaches to implementing MDM logic in a modern data platform.
