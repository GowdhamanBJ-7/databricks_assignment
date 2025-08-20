Databricks Assignment 🚀

This project demonstrates an end-to-end ETL pipeline in Databricks with multi-layer architecture (Source → Bronze → Silver → Gold) and an API ingestion pipeline using PySpark & Delta Lake.

📂 Project Structure
databricks_assignment/
│
├── source_to_bronze/
│   ├── utils.py / utils notebook   # Reusable helper functions
│   └── employee_source_to_bronze   # Driver notebook: reads raw CSVs → Bronze
│
├── bronze_to_silver/
│   └── employee_bronze_to_silver   # Cleansing & schema enforcement → Silver
│
├── silver_to_gold/
│   └── employee_silver_to_gold     # Transformations & aggregations → Gold
│
├── api_ingestion/
│   └── person_info_pipeline        # API pipeline from ReqRes → Delta
│
└── README.md

ETL Pipeline
1️⃣ Source → Bronze

Input:

Country-Q1.csv, Department-Q1.csv, Employee-Q1.csv

Process:

Read CSV files with schema inference

Store raw datasets in catalog:
/source_to_bronze/employee.csv
/source_to_bronze/department.csv
/source_to_bronze/country.csv

2️⃣ Bronze → Silver

Steps:

Read bronze files with custom schema
Convert column names from CamelCase → snake_case (UDF)
Add load_date column with current date
Write as Delta Table:

DB: Employee_info
Table: dim_employee
Path: /silver/Employee_info/dim_employee

3️⃣ Silver → Gold

Transformations:
Salary by department (descending order)
Employee counts per department per country
Department names with corresponding country names
Average employee age per department
Add at_load_date column for current_date

Question-2
🌐 API Ingestion (ReqRes)

Source API: https://reqres.in/api/users

Process:

Fetch data dynamically (pagination until empty)

Drop unnecessary fields: page, per_page, total, total_pages, support

Apply custom schema & flatten JSON

Derive new column site_address from email domain (reqres.in)

Output:

Write to Delta:
DB: site_info
Table: person_info
Path: /site_info/person_info

🛠️ Tech Stack

Databricks (PySpark, Delta Lake)

DBFS for data storage

✅ Commit History

ETL pipeline (CSV → Bronze → Silver → Gold)

API pipeline (ReqRes → Delta Lake)
Python for API handling & UDFs

SQL / DataFrames for transformations
Add load_date column
