# Databricks Notebook Pipeline — Explanation

## Purpose
This pipeline demonstrates how Databricks PySpark notebooks process BRONZE data into SILVER and GOLD layers using full MDM logic.  
The goal is to show how code‑driven transformations provide deeper control, transparency, and flexibility compared to ADF.

---

## What the Pipeline Does

### 1. Reads BRONZE Delta Files
The notebooks load standardized BRONZE outputs for:
- customers
- orders
- products

These files are already schema‑aligned by ADF.

---

### 2. Applies Advanced MDM Transformations

#### Deduplication
Using PySpark window functions:
- row_number()
- dense_rank()
- ordering by timestamps

This ensures only one surviving record per entity.

#### Identity Resolution
Keys used:
- customer_id
- order_id
- product_id

The notebook resolves identity conflicts and ensures referential integrity.

#### Survivorship Rules
Rules applied:
- latest record wins
- non‑null values preferred
- business‑specific attribute selection

#### Data Quality Enforcement
- null handling
- invalid value replacement
- type normalization

---

### 3. Writes SILVER and GOLD Delta Tables

#### SILVER Layer
Cleaned, deduped, identity‑resolved data.

#### GOLD Layer
Business‑ready models:
- Customer Golden Record
- Daily Sales Summary
- Product Performance Model

These tables are optimized for analytics.

---

## Why Databricks Is Used
Databricks notebooks are ideal for:
- complex transformations
- MDM logic
- golden record creation
- debugging and transparency
- Delta Lake optimization
- scalable processing

This makes Databricks the preferred tool for SILVER and GOLD layers.

---

## Summary
Databricks demonstrates how a code‑driven approach provides full MDM capabilities and advanced transformation logic.  
This file exists to explain the Databricks portion of the comparison project.
