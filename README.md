# 🚀 AdventureWorks2017LT – Azure Migration & Analytics Project
## 📌 Overview
![Full Project Flow](https://github.com/Marwamedha/Adventure-Works-Data-Engineering-Project/blob/main/Azure%20data%20engineering%20process%20flowchart%20(1).png?raw=true)

[Open Databricks Notebook](https://adb-7405616406532583.3.azuredatabricks.net/editor/notebooks/286303941860283?o=7405616406532583)

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
![Data_Ingestion](https://github.com/Marwamedha/Azure-data-engineering/blob/main/Images/Dynamic%20Ingestion.png?raw=true)
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


## ⚙️ 📊 Visualizations

![The Power BI dashboard](https://github.com/Marwamedha/Azure-data-engineering/blob/main/Images/Azure%20migration%20dashboard.png?raw=true)

- ****
  – 📈 Sales performance metrics  
  - **💰 Product profitability analysis
  - **👥 Customer demographics & distribution

---

### 👩‍💻 Author

Marwa Medhat
Data Engineer | Azure | Databricks | PySpark | Synapse | Power BI
