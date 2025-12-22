# Adventure-Works-Data-Engineering-Project
https://adb-7405616406532583.3.azuredatabricks.net/editor/notebooks/286303941860283?o=7405616406532583

# Adventure-Works-Data-Engineering-Project
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
- **Gold Layer**: Aggregated datasets ready for BI or reporting
- **Append Mode**: Efficiently adds new data without overwriting existing tables
- **Partitioning**: Organized by `OrderDate` for performance and cost optimization  

---

## 🛠️ Project Code Highlights

### 🔹 Concatenate Customer Names
```python
from pyspark.sql.functions import concat, col, lit

df_cus = df_cus.withColumn(
    "FullName",
    concat(col("Prefix"), lit(" "), col("FirstName"), lit(" "), col("LastName"))
)

