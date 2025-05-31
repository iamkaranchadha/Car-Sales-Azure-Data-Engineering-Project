# 🚗 Car Sales Azure Data Engineering Project

This project demonstrates a full-scale Azure Data Engineering solution to ingest, process, and model car sales data using a modern data architecture. It incorporates best practices like incremental loading, medallion architecture (Bronze, Silver, Gold), dimensional modeling, and pipeline orchestration.

![1_XKy6f8aj2Pb_nW1nRtxY1Q](https://github.com/user-attachments/assets/7a25733e-08b4-4acf-a33a-e2c7dc28ffe3)

---

## 📌 Project Goals

* Ingest car sales data from a public API
* Enable incremental data loading using watermark strategy
* Implement medallion architecture with optimized storage formats (Parquet, Delta)
* Design star schema and dimensional models using PySpark
* Establish Power BI connectivity for business reporting
* Automate and schedule data pipelines for continuous operation

---


## 🧰 Tech Stack

| Layer         | Technology Used                             |
| ------------- | ------------------------------------------- |
| Ingestion     | Azure Data Factory, API, Azure SQL Database |
| Storage       | Azure Data Lake Gen2 (Bronze/Silver/Gold)   |
| Processing    | Azure Databricks (PySpark, Spark SQL)       |
| Modeling      | Star Schema, SCD Type 1                     |
| Metadata      | Unity Catalog, Unity Metastore              |
| Reporting     | Power BI (Dataset connectivity only)        |
| Orchestration | Azure Data Factory pipelines, Triggers      |

---

## 🔄 Data Flow Steps

### 1. Ingest Data from API

* Used Azure Data Factory to call a car sales API
* Loaded initial data into Azure SQL Database
* Created a watermark table and stored procedure to support incremental loading

![image](https://github.com/user-attachments/assets/d741ae2d-f037-4c6a-8c6f-5b6cec7d2bcd)



![Screenshot 2025-05-31 204849](https://github.com/user-attachments/assets/fa0ad26f-ffce-4287-bb5d-a1b6767ca88e)


### 2. Move to Bronze Layer (Raw Zone)

* Used Azure SQL DB as a source and stored the data in Data Lake’s Bronze container in Parquet format
* Retained raw historical data for traceability


![Screenshot 2025-05-31 205017](https://github.com/user-attachments/assets/ef06f450-0839-4256-a6cc-7b39de82d53f)

![image](https://github.com/user-attachments/assets/d07e341d-2110-4d89-99e0-e788bebd52ef)



### 3. Transform into Silver Layer (Cleaned Zone)

* Read raw data in Databricks using PySpark
* Applied data cleaning, joins, formatting
* Stored cleansed and enriched data in the Silver container in Parquet format

![image](https://github.com/user-attachments/assets/ee0cd41b-c552-4108-98e8-bc0040d9901d)


![Screenshot 2025-05-31 205110](https://github.com/user-attachments/assets/34749db8-1c52-4465-a0c8-5600ef37a8a7)

![image](https://github.com/user-attachments/assets/e2171aa9-8cb6-4db3-8378-c23dc0b13e5d)


### 4. Gold Layer (Business Model)

* Used Databricks notebooks with an incremental flag parameter to support:

  * Initial load
  * Incremental load logic (idempotent)
* Created SCD Type 1 dimensions and fact tables (star schema)
* Stored business-ready data in the Gold layer in Delta format
* Created Delta tables registered with Unity Catalog and Unity Metastore

![image](https://github.com/user-attachments/assets/bb13e1bc-0a86-447b-a179-fd8cad3624af)

![image](https://github.com/user-attachments/assets/54e1fbc7-ac96-44f4-bdb1-70a1c8ce73f6)


![Screenshot 2025-05-31 205110](https://github.com/user-attachments/assets/cca0934b-2801-40ff-96da-f40e987ca8cf)

![image](https://github.com/user-attachments/assets/e6b5dc98-a8ef-48ec-9385-89f3920d69b3)

![image](https://github.com/user-attachments/assets/82718d6f-e3b4-4e90-ad75-0186426a7fe4)






### 5. Power BI Integration

* Connected Power BI to Gold Layer Delta tables

---

## ⚙️ Pipeline Orchestration

* Created multiple Databricks notebooks for transformation logic
![Screenshot 2025-05-31 202652](https://github.com/user-attachments/assets/c4d876b9-1762-4650-8766-38540b5b7afa)

* Built modular ADF pipelines for:

  * API ingestion to Azure SQL
  * Azure SQL to Bronze
  * Notebook execution for Silver and Gold
* Designed a parent pipeline to orchestrate the entire workflow
* Configured scheduled triggers for daily automation


![Screenshot 2025-05-31 205141](https://github.com/user-attachments/assets/45ebe294-6f3d-4ef5-ba7c-9a8dfc9783a2)

---

## ✅ Key Highlights

* Supports both full and incremental loads using dynamic flags
* Built entirely on serverless/cloud-native architecture
* Clean medallion structure (Bronze, Silver, Gold) using efficient file formats
* Gold layer modeled for BI consumption with SCD Type 1 logic
* Plug-and-play ready for Power BI or any downstream analytics tool




