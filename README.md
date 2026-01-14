# 🏥 Databricks Medallion Architecture – Healthcare ETL Pipeline

This project demonstrates a **real-world, production-style ETL pipeline** built on **Azure Databricks** using the **Medallion Architecture**  
(**Bronze → Silver → Gold**).

The pipeline automatically processes hospital data when new files are uploaded and produces **analytics-ready fact and dimension tables**.

---

## 🏗️ Architecture Overview

Raw Files (ADLS Gen2)

↓

Bronze Layer (Auto Loader)

↓

Silver Layer (Clean & Deduplicate)

↓

Gold Layer (Facts & Dimensions)

---

## 📂 Project Structure
- 0001_raw_data_splitting → (Optional) Split large raw files
- 0002_bronze → Incremental ingestion using Auto Loader
- 0003_silver → Clean, deduplicate & merge data
- 0004_gold → Business-level fact & dimension tables


---

## 🥉 Bronze Layer – Raw Ingestion

**Purpose:** Ingest raw data safely and incrementally.

- Reads CSV files from `raw/chunks`
- Uses **Auto Loader** with checkpointing
- Processes **only new files**
- Stores data as **Delta Lake**

📘 Notebook:
0002_bronze


---

## 🥈 Silver Layer – Curated Data

**Purpose:** Create a trusted and clean dataset.

- Cleans and standardizes hospital data
- Removes duplicates using business key (`facility_id`)
- Uses **MERGE INTO** for incremental updates
- Produces a curated hospital table

📘 Notebook:
0003_silver


---

## 🥇 Gold Layer – Analytics Ready

**Purpose:** Enable reporting and decision-making.

- Builds **analytics-ready** tables
- Creates **state-level KPIs** and hospital metrics
- Produces **Fact & Dimension** tables
- Optimized for BI tools (Power BI, Tableau)

📘 Notebook:
0004_gold


---

## 🔄 Orchestration – How It Runs Automatically

The entire pipeline is orchestrated using **Databricks Jobs**:

1. 🥉 Bronze ingestion  
2. 🥈 Silver processing  
3. 🥇 Gold aggregation  

The job runs on a **schedule** and processes new data end-to-end  
➡️ **No manual notebook execution required**

---

## ▶️ How to Run This Project

1️⃣ Upload CSV files to:
raw/chunks/

2️⃣ Clone this repo into **Databricks Repos**

3️⃣ Update storage paths (ADLS Gen2) in notebooks

4️⃣ Create a **Databricks Job** with task order: Bronze → Silver → Gold


5️⃣ Run the job or schedule it (e.g. every 30 minutes)

🎉 That’s it! The pipeline will now run automatically.

---

## 🧠 What You Will Learn

- Medallion Architecture (Bronze / Silver / Gold)
- Incremental data processing with Auto Loader
- Delta Lake MERGE patterns
- Databricks Job orchestration
- Real-world ETL pipeline design

---

## 🚀 Tech Stack

- Azure Databricks  
- PySpark  
- Delta Lake  
- Unity Catalog  
- ADLS Gen2  
- Databricks Jobs  

---

## 👨‍💻 Author

**Rahul Gupta**  
GitHub: https://github.com/gupta0096  

---

⭐ If you find this project helpful, feel free to star the repo!



