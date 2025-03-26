# Open Table Formats: Revolutionizing Data Engineering

## 📌 Overview
Open Table Formats have transformed the data engineering landscape, offering enhanced **performance, schema enforcement, data versioning, and real-time processing** capabilities. This guide provides insights into Open Table Formats, their importance, and practical implementation using **Delta Lake**.

## 🚀 Evolution of Data Engineering & Open Table Formats
- Traditional data engineering relied on **SQL-based OLAP databases (Data Warehouses)**.
- The rise of **Big Data** introduced challenges like **variety, velocity, and schema changes**, making SQL databases inefficient.
- **Data Lakes** emerged to store **structured, semi-structured, and unstructured data** at a lower cost.
- However, Data Lakes lacked **indexing, ACID transactions, and schema enforcement**, leading to performance bottlenecks.
- **Open Table Formats** bridge the gap, combining **Data Warehouse** capabilities with the **scalability of Data Lakes**.

## 🔥 Why Open Table Formats Matter?
- **Schema Enforcement** 🛠️: Ensures data consistency.
- **Data Versioning & Time Travel** ⏳: Enables restoring previous versions.
- **Indexing & Query Optimization** ⚡: Improves performance.
- **Streaming Support** 🚀: Handles real-time data ingestion.

## 📖 Popular Open Table Formats
| Format          | Best Used With |
|---------------|--------------|
| **Apache Iceberg** | AWS, Netflix |
| **Delta Lake** | Databricks, Azure |
| **Apache Hudi** | Real-time updates |

## ⚙️ Setting up Delta Lake on Databricks
1. **Create a Databricks Community Edition Account**.
2. **Upload Data** to **Databricks File System (DBFS)**.
3. **Use Spark APIs** to read/write Delta Tables.

## 🏗️ Understanding Delta Lake Architecture
- **Delta Format = Parquet + Transaction Log (`_delta_log`)**.
- **Transaction Log (`.json` files)** records inserts, updates, deletes.
- **Partitioning & Indexing** optimize performance.

## 📂 Implementing Open Table Formats (Delta Lake)
### **1️⃣ Reading a CSV file into a Spark DataFrame**
```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("DeltaExample").getOrCreate()
df = spark.read.format("csv").option("header", "true").load("data.csv")
df.show()
```

### **2️⃣ Writing Data as a Delta Table**
```python
df.write.format("delta").save("/delta/my_delta_table")
```

### **3️⃣ Querying Delta Table**
```python
delta_df = spark.read.format("delta").load("/delta/my_delta_table")
delta_df.show()
```

## 🕵️ Data Versioning & Time Travel
### **Check Table History**
```sql
DESCRIBE HISTORY my_delta_table;
```
### **Query a Previous Version**
```sql
SELECT * FROM my_delta_table VERSION AS OF 2;
```

## 📜 Schema Enforcement & Evolution
- **Schema Enforcement**: Prevents invalid data insertions.
- **Schema Evolution**: Allows schema modifications dynamically.

## 🔄 Performing DML Operations on Delta Tables
### **Insert Data**
```sql
INSERT INTO my_delta_table VALUES (1, 'Alice', 5000);
```
### **Update Data**
```sql
UPDATE my_delta_table SET salary = 6000 WHERE id = 1;
```
### **Delete Data**
```sql
DELETE FROM my_delta_table WHERE id = 1;
```

## ❌ Soft Deletes & Hard Deletes (Vacuum Command)
- **Deletes do not physically remove data**; they mark it as **"removed"**.
- **Hard deletion** using `VACUUM` removes old Parquet files.

### **Vacuum Old Data**
```sql
VACUUM my_delta_table RETAIN 7 DAYS;
```
### **Force Immediate Deletion**
```sql
SET spark.databricks.delta.retentionDurationCheck.enabled = false;
VACUUM my_delta_table RETAIN 0 HOURS;
```
⚠️ **Warning:** Once vacuumed, data **CANNOT** be recovered.

## 🎯 Conclusion
Open Table Formats, especially **Delta Lake**, are **revolutionizing data engineering** by combining **scalability, reliability, and flexibility**. Mastering them is crucial for modern **Data Engineers**.

✅ **Happy Learning!** 🚀
