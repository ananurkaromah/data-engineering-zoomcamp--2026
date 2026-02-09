# Module 3 Homework: data_warehouse

This document contains the complete solutions for **Module 3 Homework**  
(Data Engineering Zoomcamp 2026 – DataTalksClub).

All commands, SQL queries, and answers are included directly in this Markdown file as required.

---

##  Ana Nurkaromah

- Homework: Modul_03_data_warehouse
- Topic: practice working with BigQuery and Google Cloud Storage
- Dataset: we will be using the Yellow Taxi Trip Records for January 2024 - June 2024 (not the  entire year of data).
Parquet Files are available from the New York City Taxi Data found here:
https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

BIG QUERY SETUP:
Create an external table using the Yellow Taxi Trip Records.
Create a (regular/materialized) table in BQ using the Yellow Taxi Trip Records (do not partition or cluster this table).


## Question 1  
**What is count of records for the 2024 Yellow Taxi Data?**

✅ **Answer:**  
**20,332,093**

---

## Question 2  
**What is the estimated amount of data that will be read when this query is executed on the External Table and the Table?**

✅ **Answer:**  
**0 MB for the External Table and 0 MB for the Materialized Table**

---

## Question 3  
**Why are the estimated number of Bytes different?**

✅ **Answer:**  
BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (`PULocationID`, `DOLocationID`) requires reading more data than querying one column (`PULocationID`), leading to a higher estimated number of bytes processed.

---

## Question 4  
**How many records have a `fare_amount` of 0?**

✅ **Answer:**  
**8,333**

---

## Question 5  
**What is the best strategy to make an optimized table in BigQuery if your query will always filter based on `tpep_dropoff_datetime` and order the results by `VendorID`?**

✅ **Answer:**  
Partition by `tpep_dropoff_datetime` and cluster on `VendorID`.

---

## Question 6  
**Write a query to retrieve the distinct VendorIDs between `2024-03-01` and `2024-03-15` (inclusive). Compare the estimated bytes processed between the materialized table and the partitioned table. What are these values?**

✅ **Answer:**  
**310.24 MB for the non-partitioned (materialized) table and 26.84 MB for the partitioned table**

---

## Question 7  
**Where is the data stored in the External Table you created?**

✅ **Answer:**  
**GCP Bucket**

---

## Question 8  
**It is best practice in BigQuery to always cluster your data.**

✅ **Answer:**  
**False**

Clustering should be applied only when it aligns with query access patterns. Unnecessary clustering can increase cost and complexity without performance benefits.

---

## Question 9  
**Write a `SELECT COUNT(*)` query from the materialized table. How many bytes does it estimate will be read? Why?** *(Not graded)*

### Query
```sql
SELECT COUNT(*)
FROM `your_project.your_dataset.yellow_taxi_materialized`;
```
✅ **Answer:**  
**Estimated Bytes Read 0 MB (or very close to 0 MB)**
**Explanation : BigQuery can compute COUNT(*) using table metadata without scanning the underlying data. Since no columns are accessed, BigQuery does not need to read any data blocks, resulting in zero bytes processed.**