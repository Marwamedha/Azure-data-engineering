# Azure data migration

🚀 AdventureWorks2017LT – Azure Migration & Analytics Project
📌 Overview

This project demonstrates an end-to-end migration and analytics pipeline for the AdventureWorks2017LT dataset, moving data from an on-premises SQL Server environment to the Microsoft Azure cloud.

The architecture leverages Azure-native data engineering services to build a scalable, secure, and analytics-ready platform. Data is ingested, transformed, modeled, and visualized following industry best practices used in real enterprise environments.

Key Services Used:

Azure Data Factory (ADF) – data ingestion & orchestration

Azure Data Lake Storage Gen2 – centralized cloud storage

Azure Databricks – scalable data transformation using PySpark

Azure Synapse Analytics – analytical querying & modeling

Power BI – business intelligence & reporting

🏗️ Architecture

The solution follows the Medallion Architecture, which organizes data into Bronze, Silver, and Gold layers, ensuring data quality, scalability, and optimized analytics.

🧱 Bronze Layer

Stores raw ingested data exactly as received

Data is landed in Azure Data Lake Storage Gen2

Acts as the system of record

🧱 Silver Layer

Data is cleaned, validated, and enriched

Business rules are applied using Azure Databricks

Ensures high-quality, structured data

🧱 Gold Layer

Contains aggregated and analytics-ready datasets

Optimized for reporting and querying

Consumed by Azure Synapse Analytics & Power BI

🧩 Components Used

Azure Data Factory
Ingests data from the on-premises SQL Server using a self-hosted Integration Runtime.

Azure Data Lake Storage Gen2
Serves as the central data repository for all medallion layers.

Azure Databricks
Performs data transformation, cleansing, enrichment, and aggregation using PySpark and Delta Lake.

Azure Synapse Analytics
Enables analytical querying through Serverless SQL Pools and external tables.

Power BI
Provides interactive dashboards and business insights.

Microsoft Entra ID (Azure AD)
Manages authentication and access control.

Azure Key Vault
Secures credentials, secrets, and connection strings.

🔁 Steps to Reproduce
🔹 Prerequisites

Active Azure Subscription

AdventureWorks2017LT on-premises SQL Server dataset

Power BI Desktop

Basic knowledge of Azure & SQL

⚙️ Implementation
1️⃣ Data Ingestion

Configure ADF Self-Hosted Integration Runtime

Create pipelines to ingest data from on-prem SQL Server

Store raw data in the Bronze layer (ADLS Gen2)

2️⃣ Data Transformation

Using Azure Databricks notebooks:

Clean and standardize raw data

Enrich datasets with business logic

Transform Silver data into Gold aggregations

3️⃣ Data Loading

Load Gold layer data into Azure Synapse Analytics

Create Serverless External Tables

Enable fast analytical queries

4️⃣ Reporting & Visualization

Build interactive dashboards using Power BI

Analyze:

Sales trends

Customer distribution

Product profitability

🔗 Interactive Dashboard:
https://app.powerbi.com/groups/me/reports/67027b84-cbd6-42a6-bb27-7ac9f18b7d33/ReportSection?experience=power-bi

5️⃣ Security & Governance

Authentication using Microsoft Entra ID

Secrets & credentials stored in Azure Key Vault

Secure access to data lake, Databricks, and Synapse

⭐ Key Highlights

Cost-Efficient Design
Uses serverless and scalable Azure services to optimize cost.

Secure Data Management
Implements Azure-native security best practices.

Scalable Pipeline
Designed to handle enterprise-scale datasets with ease.

Industry-Standard Architecture
Medallion architecture aligned with modern data platforms.

📊 Visualizations

The Power BI dashboard includes:

📈 Sales performance metrics

💰 Product profitability analysis

👥 Customer demographics & distribution

👩‍💻 Author

Marwa Medhat
Data Engineer | Azure | Databricks | PySpark | Synapse | Power BI

![Full Project Flow](https://github.com/Marwamedha/Adventure-Works-Data-Engineering-Project/blob/main/Azure%20data%20engineering%20process%20flowchart%20(1).png?raw=true)

🔗 [Open Databricks Notebook](https://adb-7405616406532583.3.azuredatabricks.net/editor/notebooks/286303941860283?o=7405616406532583)

[Azure Databricks Notebook Link](https://adb-7405616406532583.3.azuredatabricks.net/editor/notebooks/286303941860283?o=7405616406532583)

# 📦 Retail & Sales ETL Project – Azure Databricks

## 🚀 Project Overview
This project demonstrates the full ETL lifecycle for the **AdventureWorks** dataset using **Azure Databricks**, **PySpark**, and **Azure Data Lake Storage Gen2**.

### 🔍 Objectives:
- Load and transform retail CSV/Parquet data into a **Delta Lake data warehouse**.
- Apply column transformations and cleansing for accurate analytics.
- Perform aggregations to derive business metrics like **total orders per day**.
- Automate data storage and management in **Silver/Gold layers** of the data lake.

---

## ⚙️ Technologies Used
- **Azure Databricks** – Notebook development and Spark processing  
- **PySpark** – DataFrame transformations, aggregations, and cleansing  
- **Azure Data Lake Storage Gen2** – Data storage (Parquet & Delta)  
- **Delta Lake** – ACID-compliant storage for reliable ETL pipelines  
- **Python** – Scripting, functions, and logic  

---

## 🧠 Key ETL Features

### 🔄 ETL Flow:
- **Source**: AdventureWorks raw datasets (sales, customers, returns, products)  
- **Transformations**:
  - Column concatenation and renaming (e.g., full customer name)
  - Data cleansing (e.g., removing nulls, correcting formats)
  - Aggregations (e.g., total orders per day)
  - Sorting, filtering, and ranking
- **Destination**: Silver and Gold layers in Delta/Parquet formats on ADLS Gen2  

### 🕵️‍♀️ Data Quality & Checks:
- Ensures all numeric columns are valid
- Removes duplicate records
- Handles missing or inconsistent values  

---

## 🧱 Delta Lake & Parquet Layering

- **Silver Layer**: Cleansed and enriched data from raw sources  
  - [Explore Silver Layer Notebook](https://github.com/Marwamedha/Adventure-Works-Data-Engineering-Project/blob/main/Sliver_layer.ipynb)
- **Gold Layer**: Aggregated datasets ready for BI or reporting
- **Append Mode**: Efficiently adds new data without overwriting existing tables
- **Partitioning**: Organized by `OrderDate` for performance and cost optimization  

---

## 🛠️ Project Code Highlights

### 🔹 Concatenate Customer Names
```python
# AdventureWorks ETL Pipeline – All Code in One Cell

from pyspark.sql import SparkSession
from pyspark.sql.functions import concat, col, lit, regexp_replace, count

# -----------------------------
# 1️⃣ Create Spark Session
# -----------------------------
spark = SparkSession.builder \
    .appName("AdventureWorks ETL") \
    .getOrCreate()

# -----------------------------
# 2️⃣ Load Raw Data
# -----------------------------
# Example paths, update to your ADLS Gen2 paths
df_cus = spark.read.format("csv").option("header", True).load("/mnt/raw/Customer.csv")
df_sales = spark.read.format("csv").option("header", True).load("/mnt/raw/Sales.csv")

# -----------------------------
# 3️⃣ Transformations
# -----------------------------

# Concatenate full customer name
df_cus = df_cus.withColumn(
    "FullName",
    concat(col("Prefix"), lit(" "), col("FirstName"), lit(" "), col("LastName"))
)

# Replace 'S' with 'T' in OrderNumber
df_sales = df_sales.withColumn(
    'OrderNumber',
    regexp_replace(col('OrderNumber'), 'S', 'T')
)

# -----------------------------
# 4️⃣ Aggregations
# -----------------------------
df_order_agg = df_sales.groupBy("OrderDate") \
    .agg(count("OrderNumber").alias("Total_order"))

# Show aggregated results
df_order_agg.display()

# -----------------------------
# 5️⃣ Write to ADLS Gen2 (Delta format)
# -----------------------------
df_sales.write.format("delta") \
    .mode("append") \
    .save("abfss://silver@awstoragedeltalake1.dfs.core.windows.net/AdventureWorks_Returns")

average_score = sum(student_marks[query_name])/len(student_marks[query_name])
print(f"\nAverage score for {query_name}: {average_score:.2f}")
