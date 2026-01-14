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

## 📸 Pipeline Execution – End-to-End Proof (Visual Walkthrough)

This section visually demonstrates how the pipeline behaves in **real-world conditions**, from manual execution to fully automated incremental processing.

---

### 🟢 Initial Run – When 5 Files Exist in `raw/chunks`

**Source:**  
At the beginning, the `raw/chunks` folder contains **5 CSV files** (raw hospital data).

<img width="2894" height="778" alt="Raw files in chunks folder" src="https://github.com/user-attachments/assets/2ba51b3f-f8e1-4367-b8a0-805f5629350a" />

---

### ▶️ Manual Pipeline Execution (First Run)

The Databricks Job is triggered manually to validate the full pipeline.

<img width="3054" height="510" alt="Manual job run" src="https://github.com/user-attachments/assets/ab831bbc-9a28-44b7-a352-64a1eaf0119e" />

<img width="2010" height="442" alt="Bronze Silver Gold job success" src="https://github.com/user-attachments/assets/ec261c4d-f15c-4459-83cc-6e4ab3076ed6" />

✔ Bronze ingests raw files  
✔ Silver cleans and deduplicates  
✔ Gold creates analytics tables  

---

### 🥇 Data Successfully Loaded into Gold Tables

After the pipeline completes, data is available in **Gold fact and dimension tables**.

<img width="2984" height="928" alt="Gold tables populated" src="https://github.com/user-attachments/assets/c9c899b3-22af-47bd-9a94-f80e1da1824e" />

---

## 🔄 Incremental Load – New Files Arrive Automatically

Now, **new files are uploaded** to the `raw/chunks` folder.
<img width="2910" height="898" alt="New raw files added" src="https://github.com/user-attachments/assets/8c13b863-7a7d-4407-b586-6881354e7672" />
Auto-loaded into bronze/hospitals as Delta Lake (Parquet-based) format.
<img width="2912" height="1018" alt="image" src="https://github.com/user-attachments/assets/4dc5bc93-9e86-4a31-ac7a-945a596a7625" />

📌 **Important:**  
The pipeline is **not reprocessing old files** — only new files are detected.

---

### ⚙️ Automated Job Triggered (No Manual Action)

The scheduled Databricks Job runs automatically and processes **only the newly added files**.

<img width="3046" height="426" alt="Job triggered automatically" src="https://github.com/user-attachments/assets/ff8a51d4-017e-40de-bf5e-76cfa2eaab07" />

<img width="3004" height="1270" alt="Job run success" src="https://github.com/user-attachments/assets/13353575-651f-43d9-8e2e-26da328ca9d3" />

✔ Incremental ingestion  
✔ Safe re-runs  
✔ No duplicates  

---

### ✅ Gold Tables Updated with New Data

Finally, the Gold tables reflect **only the new incoming data**, confirming correct incremental behavior.

<img width="2994" height="1028" alt="Gold tables updated" src="https://github.com/user-attachments/assets/37dee11b-b9ac-4b90-98f8-5c6bc4637e7d" />

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



