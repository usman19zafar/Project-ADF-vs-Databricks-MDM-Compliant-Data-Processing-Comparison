# Project-ADF-vs-Databricks-MDM-Compliant-Data-Processing-Comparison
A technical comparison of two modern data‑engineering approaches for processing customer, orders, and product datasets through an MDM‑aligned pipelines.

## Overview
This repository compares two modern approaches for processing customer, orders, and product datasets using Master Data Management (MDM) principles.  
Both pipelines implement the same RAW → BRONZE → SILVER → GOLD logic, but with different technologies:

- Azure Data Factory (ADF) Data Flows  
- Databricks PySpark Notebooks  

The goal is to show how each platform handles identical transformations, highlight strengths and limitations, and provide a clear architectural comparison for data engineers and architects.

---

## Datasets
Three sample datasets are used throughout both pipelines:

- **customers.csv**  
- **orders.csv**  
- **products.csv**

Each dataset contains intentional inconsistencies to demonstrate schema drift handling, deduplication, and identity resolution.

---

## Processing Approach

### ADF Data Flow Pipeline
ADF is used to implement the pipeline visually through Data Flows.  
Key responsibilities:
- RAW → BRONZE processing  
- Schema drift handling  
- Column standardization  
- Type casting  
- Basic deduplication using window logic  
- Landing Delta files  

This approach demonstrates UI‑driven ETL/ELT with minimal coding.

---

### Databricks Notebook Pipeline
Databricks implements the same logic using PySpark notebooks.  
Key responsibilities:
- BRONZE → SILVER → GOLD transformations  
- Window‑based dedupe  
- Identity resolution  
- Null handling  
- Business rule enforcement  
- Delta Lake optimization  

This approach demonstrates code‑driven ELT with full control and transparency.

---

## MDM Compliance

Both pipelines enforce core Master Data Management principles:

### Identity Resolution
- Keys: customer_id, order_id, product_id  
- Partition‑based dedupe  
- Latest‑record survivorship  

### Schema Standardization
- Consistent column naming  
- Type enforcement  
- Drift handling  

### Deduplication
- ADF: window + rowNumber  
- Databricks: advanced window logic  

### Golden Record Creation
- Performed in GOLD layer  
- Combines survivorship, business rules, and validated attributes  

### Auditability
- ADF: pipeline logs  
- Databricks: Delta Lake versioning (time travel)  

---

## Repository Structure

```code

├── README.md
│
├── datasets/
│   ├── customers.csv
│   ├── orders.csv
│   └── products.csv
│
├── adf/
│   ├── df_mini_screenshot.png
│   ├── pipeline.json
│   ├── dataflow_raw_to_bronze.json
│   └── explanation.md
│
├── databricks/
│   ├── pipeline2_screenshot.png
│   ├── silver_transformations.py
│   └── gold_models.py
│
└── comparison/
├── comparison.md
└── mdm_principles.md
```

---

## Comparison Summary

### ADF Data Flow
**Strengths**
- Excellent for ingestion  
- Handles schema drift  
- Visual transformations  
- Easy orchestration  

**Limitations**
- UI inconsistencies  
- Harder debugging  
- Limited complex logic  

---

### Databricks Notebooks
**Strengths**
- Full control with PySpark  
- Advanced window functions  
- Delta Lake optimization  
- Ideal for SILVER/GOLD logic  

**Limitations**
- Requires coding  
- More setup effort  

---

## Purpose of This Project
This repository is designed for:
- data engineers  
- architects  
- students  
- interview preparation  
- portfolio demonstration  

It shows how two major Azure tools solve the **same MDM problem** in different ways.

---

## How to Run

1. Upload RAW CSVs to your storage account  
2. Import ADF pipeline and Data Flows  
3. Import Databricks notebooks  
4. Run each pipeline independently  
5. Compare BRONZE, SILVER, and GOLD outputs  

---

## License
MIT License

