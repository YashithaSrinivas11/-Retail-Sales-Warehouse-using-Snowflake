
# 🧊 Real-Time Retail Analytics using Snowflake Snowpipe & Azure Storage



## 📌 Project Summary
This project demonstrates how to design and implement a mini data warehouse using **Snowflake** to analyze retail sales across products, customers, and time periods. Built as a student portfolio project, it showcases dimensional modeling, SQL querying, and cloud data warehousing best practices.Also automated data ingestion in Snowflake using Snowpipe and Azure Blob Storage.

## 🧠 Objective
Build a data warehouse to answer key business questions such as:
- Which products generate the most revenue?
- What is the monthly trend in sales?
- How do different customer age groups perform in terms of spending?

---

## 🗃️ Schema Design

This project uses a **star schema** with:
- **FACT_SALES** (fact table)
- **DIM_PRODUCT**, **DIM_CUSTOMER**, **DIM_TIME** (dimension tables)

![Schema Diagram](snowflake_star_schema.png)

---

## 📂 Data Files
| File Name          | Table Name     | Description                      |
|-------------------|----------------|----------------------------------|
| `dim_product.csv`  | DIM_PRODUCT    | Product details                  |
| `dim_customer.csv` | DIM_CUSTOMER   | Customer info with age/location |
| `dim_time.csv`     | DIM_TIME       | Date breakdowns                 |
| `fact_sales.csv`   | FACT_SALES     | Transaction-level sales data    |

---

## 💻 Technologies Used
- ❄️ **Snowflake** (on Azure, Pune)
- 🐍 Python (for data generation)
- 📄 CSV files (local upload)
- 🧾 SQL (Joins, Group By, Aggregates)

---

## 📊 Key SQL Queries & Insights

### 🔹 Total Sales per Product
```sql
SELECT 
  p.name AS product_name,
  SUM(f.quantity) AS total_units_sold,
  SUM(f.total_amount) AS total_revenue
FROM FACT_SALES f
JOIN DIM_PRODUCT p ON f.product_id = p.product_id
GROUP BY p.name
ORDER BY total_revenue DESC;
```

### 🔹 Monthly Sales Trend
```sql
SELECT 
  t.month,
  SUM(f.total_amount) AS monthly_revenue
FROM FACT_SALES f
JOIN DIM_TIME t ON f.time_id = t.time_id
GROUP BY t.month;
```

### 🔹 Sales by Customer Age Group
```sql
SELECT 
  c.age_group,
  SUM(f.total_amount) AS total_sales
FROM FACT_SALES f
JOIN DIM_CUSTOMER c ON f.customer_id = c.customer_id
GROUP BY c.age_group
ORDER BY total_sales DESC;
```


---

## 📈 Future Improvements
- Add new dimensions like Store or Region
- Automate data ingestion using Snowpipe(Completed)
- 🔄 Snowflake Snowpipe Integration (Azure Blob Storage)
This project demonstrates how to automate data ingestion in Snowflake using Snowpipe and Azure Blob Storage.

✅ Connected Snowflake to an external stage using a secure SAS token

✅ Created a Snowflake stage pointing to Azure Blob container

✅ Defined a Snowpipe to load data into the FACT_SALES table automatically

✅ Triggered the Snowpipe using ALTER PIPE ... REFRESH to test ingestion

✅ Verified updated query results reflecting newly loaded data

This setup simulates a real-world streaming ingestion pipeline, enabling seamless cloud-based ETL.
![Screenshot (78)](https://github.com/user-attachments/assets/8fb21ca1-1773-483d-9faf-8c965b41c6d6)
![Screenshot (77)](https://github.com/user-attachments/assets/1646a851-4e35-4124-bff4-91fbc77046f0)
![Screenshot (76)](https://github.com/user-attachments/assets/7f7e2085-e063-4460-8e77-227e1ed4208b)



- Build dashboards with Power BI or Streamlit

---

## 📁 Folder Structure
```
snowflake-retail-sales-warehouse/
├── data/
│   ├── dim_product.csv
│   ├── dim_customer.csv
│   ├── dim_time.csv
│   └── fact_sales.csv
├── sql/
│   └── analysis_queries.sql
├── screenshots/
│   └── [add your screenshots here]
├── snowflake_star_schema.png
└── README.md
```
