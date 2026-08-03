# Databricks Bootcamp (Medallion Architecture)

## Overview
This project migrates my previous [Data Warehouse](https://github.com/Molo-M/sql-data-warehouse-project) onto a **Data Lakehouse on Databricks**, migrating a traditional SQL Server relational warehouse into a scalable, cloud-native Delta Lake pipeline. Using a three-tier **Medallion Architecture** (Bronze, Silver, Gold), raw enterprise CRM and ERP data is ingested, cleansed, and transformed into a production-ready Star Schema for downstream analytics.

---

## Architecture & Data Flow


```

+------------------+      +-------------------+      +-------------------+      +--------------------+
|  Raw Source Data | ---> |   Bronze Layer    | ---> |   Silver Layer    | ---> |     Gold Layer     |
| (CRM & ERP CSVs) |      | (Raw Delta Tables)|      | (Cleaned/Conformed|      | (Star Schema /     |
+------------------+      +-------------------+      |   Delta Tables)   |      |  Analytics Views)  |
+-------------------+      +--------------------+

```

- **Bronze Layer (Raw):** Ingests raw CSV source files directly into Delta format with schema preservation and metadata logging.
- **Silver Layer (Cleaned):** Handles data cleansing, standardization, null handling, data type casting, and deduplication.
- **Gold Layer (Curated):** Models clean data into dimension (`dim_`) and fact (`fact_`) tables structured into a Star Schema optimized for BI queries and reporting.

---

## Tech Stack
- **Platform:** Databricks (Community / Azure / AWS)
- **Storage & Table Format:** Delta Lake (`.parquet` + `_delta_log`)
- **Languages:** PySpark / Spark SQL / Python
- **Orchestration:** Databricks Workflows (Jobs)
- **Modeling:** Dimensional Data Modeling (Star Schema, Fact & Dimension tables)

---

## Workflow & Execution

The pipeline is automated using **Databricks Workflows**:

1. `bronze`: Reads raw CSV files from storage and writes append-only Delta tables.
2. `silver`: Reads Bronze tables, cleans messy columns, applies business logic validation, and overwrites/merges into Silver Delta tables.
3. `gold`: Constructs analytical Fact and Dimension tables from Silver layer data.

---

## Credits & Acknowledgments

The core data requirements and business logic for this project were adapted from the Databricks 2 day Bootcamp by [Data with Baraa](https://www.youtube.com/@DataWithBaraa). The architecture was fully re-engineered and migrated from a traditional SQL Server setup into a cloud Data Lakehouse using **Databricks, PySpark, and Delta Lake**.

```

```
