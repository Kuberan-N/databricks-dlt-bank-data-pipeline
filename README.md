# databricks-dlt-bank-data-pipeline
End-to-end Databricks data engineering project implementing Medallion Architecture, Auto Loader ingestion, DLT transformations, CDC pipelines, and Gold-layer analytics.


-- Project Overview

This project demonstrates an end-to-end data engineering pipeline built on Databricks using the Lakehouse architecture.

The pipeline ingests raw banking data from CSV files, performs data quality validation and transformations, applies Slowly Changing Dimension (SCD) logic, and produces curated datasets for analytics and reporting.

The project simulates a real-world data platform where customer and transaction data flows through multiple processing layers before becoming analytics-ready.

-- Architecture

The pipeline follows the **Medallion Architecture** pattern commonly used in modern lakehouse platforms.

Landing → Bronze → Silver → Gold

Each layer has a specific responsibility:

- Landing Layer – Incremental ingestion using Auto Loader
- Bronze Layer – Data cleaning and quality validation using DLT Expectations
- Silver Layer – Data transformation and dimensional modeling
- Gold Layer – Business-level aggregations used for analytics and reporting

  -- Technologies Used

The pipeline was built using the following technologies:

- Databricks Lakehouse Platform
- Apache Spark (PySpark)
- Spark Declarative Pipelines (DLT / Lakeflow)
- Delta Lake
- Auto Loader for incremental file ingestion
- Unity Catalog for governance and data management
- Databricks Volumes as the storage layer
- Streaming Delta Tables
- CDC (Change Data Capture) using Auto CDC
- Apply Changes API for SCD Type 1 implementation
- Materialized Views and Views
- Databricks Native Dashboards for analytics
- Databricks Jobs for orchestration and scheduling

  -- Project Structure

## Project Structure

The project is organized based on the Medallion architecture and pipeline stages.

```
databricks-dlt-bank-data-pipeline
│
├── landing
│   └── landing_pipeline.py
│
├── bronze
│   └── bronze_cleaning_pipeline.py
│
├── silver
│   └── silver_transformation_pipeline.py
│
├── gold
│   └── gold_analytics_pipeline.py
│
├── dashboards
│   └── bi_dashboard.png
│
└── README.md
```

Each layer represents a stage in the data processing pipeline:

- Landing – Ingest raw data using Auto Loader
- Bronze – Data cleaning and quality checks using DLT expectations
- Silver – Business transformations and SCD implementation
- Gold – Aggregated datasets for analytics and reporting

---

## Data Pipeline Layers

The pipeline follows the Medallion Architecture where data moves through multiple stages to improve quality and usability.

### Landing Layer – Data Ingestion

The Landing layer ingests raw source data into the lakehouse.

In this project the source data is stored as CSV files in Databricks Volumes. Auto Loader is used with Structured Streaming to process files incrementally as new data arrives.

Key features implemented:

* Incremental ingestion using Auto Loader
* Schema enforcement
* Streaming Delta tables
* Databricks Volumes as the storage layer

Auto Loader allows the pipeline to automatically detect new files and process them without manual intervention.

### Bronze Layer – Data Quality and Cleaning

The Bronze layer focuses on validating and cleaning the raw data.

DLT Expectations are used to enforce data quality rules such as:

* expect_or_fail
* expect_or_drop
* expect

Examples of validations performed:

* Null checks on important columns
* Email format validation
* Phone number standardization
* Allowed value filtering
* Standardization of text fields

The pipeline also tracks validation results using the built-in Expectations monitoring dashboard in Databricks.

### Silver Layer – Data Transformation

The Silver layer performs business level transformations and prepares structured datasets.

Transformations implemented include:

* Customer age calculation
* Customer tenure calculation
* Transaction direction classification (IN / OUT)
* Channel classification (Physical / Digital)
* Date decomposition (year, month, day)

This layer converts cleaned data into analytics-ready datasets.

### Slowly Changing Dimensions

The pipeline also demonstrates handling data changes using Slowly Changing Dimensions.

SCD Type 1 is implemented using the `apply_changes()` API which updates records without maintaining history.

SCD Type 2 is implemented using `create_auto_cdc_flow()` which tracks historical changes and maintains record versions.

### Gold Layer – Business Analytics

The Gold layer produces curated datasets designed for business reporting and analytics.

A materialized view combines customer and transaction datasets to create a wide analytical table.

An aggregated table is then created to provide metrics such as:

* total accounts per customer
* total transactions
* total credits and debits
* average transaction amount
* first and last transaction dates
* channels used

These datasets are optimized for BI dashboards and analytical queries.

---


Good. The next section should be **BI Dashboard** and then **Pipeline Orchestration**. Keep them short since you already said BI was not the main focus.

Paste the following **after the Data Pipeline Layers section** in your README.

---

## BI Dashboard

To demonstrate how the curated Gold layer data can be consumed, a simple **Databricks Native Dashboard** was created.

The dashboard currently includes visualizations such as:

* Customer distribution by gender
* Total credit amount by last transaction year

These charts are built directly on top of the Gold aggregation tables created in the pipeline.

The main focus of this project was the **data engineering pipeline**, so the BI layer is intentionally kept simple to showcase how the curated datasets can support analytics and reporting.

![BI Dashboard](dashboards/bi_dashboard.png)
---

## Pipeline Orchestration

The entire pipeline is orchestrated using **Databricks Jobs**.

The job runs the Spark Declarative Pipeline end-to-end and automates the full data workflow from ingestion to analytics.

The following orchestration features were configured:

* Scheduled pipeline execution
* Job start notifications
* Job success notifications
* Job failure alerts

This ensures the pipeline can run reliably and provides visibility into pipeline execution status.


Key Learnings

This project helped strengthen my understanding of building production-style data pipelines using the Databricks Lakehouse platform.

Some of the key things I practiced while building this project:

Designing pipelines using Medallion Architecture

Implementing incremental ingestion using Auto Loader

Applying data quality rules using DLT Expectations

Building streaming tables with Structured Streaming

Implementing Slowly Changing Dimensions (SCD Type 1 and Type 2)

Creating analytics-ready Gold layer datasets

Using Databricks dashboards for quick analytics

One important learning from this project was how declarative pipelines simplify complex data workflows by allowing developers to focus more on data transformations and data quality rather than managing orchestration logic.



