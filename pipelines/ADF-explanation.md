# Azure Data Factory (ADF) Data Flow Pipeline — Explanation

## Purpose
This pipeline demonstrates how Azure Data Factory Data Flows process RAW datasets into BRONZE‑standardized Delta outputs using a visual, UI‑driven approach.  
The goal is to show how ADF handles schema drift, type enforcement, and basic MDM‑aligned transformations without requiring code.

---

## What the Pipeline Does

### 1. Reads RAW CSV Files
ADF sources the following datasets:
- customers.csv
- orders.csv
- products.csv

Each file may contain:
- inconsistent column names
- mixed data types
- duplicates
- null values

---

### 2. Applies Schema Drift Handling
ADF automatically:
- detects incoming columns
- maps them to expected schema
- aligns naming conventions
- enforces data types

This is one of ADF’s strongest capabilities.

---

### 3. Performs Basic Transformations
Each Data Flow applies:
- **Select**: column pruning and renaming  
- **Derived Columns**: type casting, normalization  
- **Filter**: removing invalid rows  
- **Window**: deduplication using rowNumber()  

These steps prepare the data for downstream processing.

---

### 4. Writes BRONZE Delta Files
The final sink writes standardized Delta tables to the BRONZE layer.  
Outputs are partitioned and ready for SILVER processing.

---

## Why ADF Is Used
ADF Data Flows are effective for:
- ingestion
- schema alignment
- drift handling
- lightweight transformations
- visual debugging
- preparing BRONZE data

ADF is not intended for complex MDM logic, but it provides a strong foundation for BRONZE standardization.

---

## Summary
ADF demonstrates how a visual, UI‑driven tool can perform RAW → BRONZE processing with schema standardization and basic MDM alignment.  
This file exists to explain the ADF portion of the comparison project.
