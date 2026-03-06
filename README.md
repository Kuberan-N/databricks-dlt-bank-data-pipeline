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

The project is organized based on the Medallion architecture and pipeline stages.

**databricks-dlt-bank-data-pipeline
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
└── README.md**

Each layer represents a stage in the data processing pipeline:

- Landing – Ingest raw data using Auto Loader
- Bronze – Data cleaning and quality checks using DLT expectations
- Silver – Business transformations and SCD implementation
- Gold – Aggregated datasets for analytics and reporting


