# Databricks Assignment 🚀  

This project demonstrates an **end-to-end ETL pipeline in Databricks** with a **multi-layer architecture** (Source → Bronze → Silver → Gold) and an **API ingestion pipeline** using PySpark & Delta Lake.  

---


## 🔄 ETL Pipeline  

### 1️⃣ Source → Bronze  
**Input:**  
- `Country-Q1.csv`  
- `Department-Q1.csv`  
- `Employee-Q1.csv`  

**Process:**  
- Read CSV files with schema inference  
- Store raw datasets in **DBFS catalog**:  
/source_to_bronze/employee.csv
/source_to_bronze/department.csv
/source_to_bronze/country.csv

---

### 2️⃣ Bronze → Silver  
**Steps:**  
- Read bronze files with **custom schema**  
- Convert **CamelCase → snake_case** using UDF  
- Add `load_date` column with current date  
- Write as Delta Table:  

DB: Employee_info
Table: dim_employee
Path: /silver/Employee_info/dim_employee
---

### 3️⃣ Silver → Gold  
**Transformations:**  
- Salary by department (descending order)  
- Employee counts per department per country  
- Department names with corresponding country names  
- Average employee age per department  
- Add `at_load_date` column with current date  

**Output:**  
/gold/employee/fact_employee


---

## 🌐 Question-2: API Ingestion (ReqRes)  

**Source API:** [https://reqres.in/api/users](https://reqres.in/api/users)  

**Process:**  
- Fetch data dynamically with **pagination** (until empty)  
- Drop unnecessary fields: `page`, `per_page`, `total`, `total_pages`, `support`  
- Apply **custom schema** & flatten JSON  
- Derive new column `site_address` from email domain (`reqres.in`)  
- Add `load_date` column  

**Output:**  
DB: site_info
Table: person_info
Path: /site_info/person_info


---

## 🛠️ Tech Stack  
- **Databricks** (PySpark, Delta Lake)  
- **DBFS** for data storage  
- **Python** for API handling & UDFs  
- **SQL / DataFrames** for transformations  

---

## ✅ Commit History  
- ETL pipeline (CSV → Bronze → Silver → Gold)  
- API pipeline (ReqRes → Delta Lake)  
- Schema standardization (camelCase → snake_case)  
- Load date tracking for auditability  

---

