# 🚖 End-to-End Rideshare Data Pipeline with Databricks, Delta Lake(Delta Tables) , Power BI & Superset

## 📌 Project Overview
This project demonstrates a **complete data engineering pipeline** built using **Databricks, PySpark, Delta Lake, PostgreSQL, Power BI, and Apache Superset**.  

The use case is analyzing **Uber/Lyft rideshare data** combined with **gas price data** to generate insights that help companies:  
- Optimize **pricing & surge multipliers**  
- Allocate drivers to **high-demand areas**  
- Increase **overall revenue**  

---

## 🛠️ Architecture (Bronze → Silver → Gold)

- **Bronze Layer** → Raw data ingested from APIs (rideshare + gas prices) and stored in **Databricks DBFS**.  
- **Silver Layer** → Data cleaning, outlier removal, statistical checks using **PySpark Notebooks**.  
- **Gold Layer** → SQL Views converted into **Delta Tables** for analytics dashboards.  

📌 The architecture follows **Medallion Architecture** best practices.

---

## ⚙️ Workflow

### 1. Data Ingestion (Bronze)
- Fetched data from APIs with **PySpark**.  
- Stored CSVs in **DBFS volumes**.  
- Registered into Databricks Catalog.  

📸 *Screenshots:*  
<img width="1670" height="846" alt="data_uploaded_databricks" src="https://github.com/user-attachments/assets/3c01bc4c-45a0-4b4d-a2ea-b948ae5fb6bb" />
![Data uploaded to Databricks](images/data_uploaded_databricks.png)  

<img width="1691" height="751" alt="csv_uploaded_schema_volume" src="https://github.com/user-attachments/assets/c5238480-a974-4a13-9291-c85d8699cf66" />
![CSV Schema Volume](images/csv_uploaded_schema_volume.png)

<img width="1875" height="865" alt="gas_price_data_uploaded" src="https://github.com/user-attachments/assets/9331e8be-9718-4292-9a84-c677684ecd7d" />
![Gas Price Data](images/gas_price_data_uploaded.png)  

<img width="1118" height="665" alt="successfull_data_uploaded" src="https://github.com/user-attachments/assets/877fc335-7391-4410-84c0-dc5864676ad6" />
![Successful Data Upload](images/successfull_data_uploaded.png)  

---

### 2. Cluster Setup & Libraries
- Created a **Databricks compute cluster**.  
- Installed required **libraries** (Postgres connector, Spark utils).  

📸 *Screenshots:*  
<img width="1918" height="545" alt="data_bricks_compute_engine " src="https://github.com/user-attachments/assets/d3da05c3-982a-4642-ac04-0f62e3d10f46" />
![Cluster Setup](images/data_bricks_compute_engine.png)  


<img width="1147" height="510" alt="db_library_installed" src="https://github.com/user-attachments/assets/e1336d63-159e-44bc-b31a-5ab628f41e7b" />
![DB Library Installed](images/db_library_installed.png)

---

### 3. Data Preprocessing (Silver)
- Used PySpark to clean and prepare data:
  - Removed null values  
  - Handled outliers (`IQR method`)  
  - Basic statistical validation  

📸 *Screenshots:*  
<img width="1058" height="128" alt="Screenshot 2025-06-27 015112" src="https://github.com/user-attachments/assets/b581f924-0de9-4baa-b8ae-8a61c63eae8e" />
![PySpark Preprocessing](images/Screenshot_2025-06-27_015112.png)  

<img width="1087" height="116" alt="Screenshot 2025-06-27 023518" src="https://github.com/user-attachments/assets/39ab1cdd-7d13-4ca7-9882-61dcf2cfa902" />
![Data Cleaning Logs](images/Screenshot_2025-06-27_023518.png)  

---

### 4. SQL Views & Gold Layer
- Created **SQL views** for:
  - Profit per ride  
  - Profit margin %  
  - Fuel expense impact  
  - Surge multiplier effects  
- Converted into **Delta Tables** for BI dashboards.  

📸 *Screenshots:*  
<img width="1918" height="800" alt="all_golden_table_created" src="https://github.com/user-attachments/assets/6d708d11-0875-4f55-9410-08e2e37cc32e" />
![All Golden Tables](images/all_golden_table_created.png)

<img width="1915" height="836" alt="data_uploaded_db" src="https://github.com/user-attachments/assets/f1bf3b14-e4b8-48eb-af1e-ced7be1476ba" />
![SQL Query Explorer](images/data_uploaded_db.png)

---

### 5. Jobs & Pipelines
- Built and automated **ETL pipelines** in Databricks Jobs.  
- Logic included daily partitioning (Silver → Bronze for a specific day).  

📸 *Screenshot:*  

<img width="1655" height="557" alt="DB_JOB" src="https://github.com/user-attachments/assets/6ac04da9-9cee-4e7c-b9c1-4662ba93984a" />
![Databricks Job Pipeline](images/DB_JOB.png)  

---

### 6. PostgreSQL Integration
- Created **ride_pricing** database in PostgreSQL.  
- Stored **cleaned rideshare table** for Superset access.  

📸 *Screenshots:*  
<img width="727" height="177" alt="Screenshot 2025-05-29 201404" src="https://github.com/user-attachments/assets/f239b5eb-5a44-4525-874a-fba551223c14" />
![Postgres Database](images/Screenshot_2025-05-29_201404.png)  

<img width="1915" height="836" alt="data_uploaded_db" src="https://github.com/user-attachments/assets/97b0cf32-7fb7-429c-8f49-0495e873ec4d" />
![Table Schema](images/data_uploaded_db.png) 

---

### 7. Visualization & BI
#### 🔹 Power BI
- Built dashboards for **profit vs gas price trends**, **cab type comparison**, and **route analysis**.  

📸 *Screenshots:*  
<img width="730" height="282" alt="Screenshot 2025-05-29 200837" src="https://github.com/user-attachments/assets/598f859e-685a-4728-8559-4dd3c1185ec9" />
![Power BI Dashboard](images/Screenshot_2025-05-29_200837.png)  

<img width="675" height="316" alt="Screenshot 2025-05-29 201346" src="https://github.com/user-attachments/assets/117c83e5-32d9-4762-b3bd-fc06fc3d268b" />
![Power BI Chart](images/Screenshot_2025-05-29_201346.png)  

#### 🔹 Apache Superset (Docker Hosted)
- Hosted Superset on Docker.  
- Created scatter plots, bar charts, and heatmaps.  
- Connected to PostgreSQL database for querying.  

📸 *Screenshot:*  
![Superset SQL Editor](images/superset_sql.png)  

#### 🔹 Ngrok for Remote Access
- Used **ngrok** to securely expose local Superset dashboards.  

📸 *Screenshot:*  

<img width="1212" height="565" alt="ngrok" src="https://github.com/user-attachments/assets/7c5bdc76-891f-4194-ae0c-9d3920436802" />
![Ngrok Hosting](images/ngrok.png)  

---

## 📈 Key Insights
- **Short rides (0–3 miles)** = bulk of total profit, though per-ride margins are thinner.  
- **Fuel costs** significantly cut profits → dynamic **fuel surcharges** can protect margins.  
- **Surge multiplier optimization** during peak demand = more revenue.  
- **Top profitable routes** (downtown → airport) should get priority driver allocation.  
- **Uber vs Lyft** → one platform showed consistently stronger margins.  

---

## 🛠️ Tech Stack
- **Databricks** (DBFS, Delta Lake, Notebooks, Jobs, Pipelines)  
- **PySpark** (ETL & preprocessing)  
- **PostgreSQL** (structured storage for BI)  
- **Power BI** (executive dashboards)  
- **Apache Superset (Docker)** (exploratory analytics dashboards)  
- **Ngrok** (secure public hosting)  

---

## 🚀 How to Run
1. Clone this repo:
   ```bash
   git clone https://github.com/your-username/rideshare-pipeline.git
