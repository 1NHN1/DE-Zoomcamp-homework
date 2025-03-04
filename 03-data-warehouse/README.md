# DE-Zoomcamp-homework


BIG QUERY SETUP:
## Create an external table using the Yellow Taxi Trip Records.

```sql
CREATE OR REPLACE EXTERNAL TABLE `dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand`
OPTIONS (
  format = 'PARQUET',
  uris = ['gs://dezoomcamp_hw3_2025_nhn/yellow_tripdata_2024-*.parquet']
);

```


## Create a (regular/materialized) table in BQ using the Yellow Taxi Trip Records (do not partition or cluster this table).

```sql
CREATE OR REPLACE TABLE `dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand_regular` AS
SELECT * FROM `dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand`

```

##  Question 1.  What is count of records for the 2024 Yellow Taxi Data?

> 20,332,093

```sql
SELECT COUNT(*) FROM `tidy-arena-443619-v0.dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand`;
--20332093
```

##  Question 2. Write a query to count the distinct number of PULocationIDs for the entire dataset on both the tables. What is the estimated amount of data that will be read when this query is executed on the External Table and the Table?

> 0 MB for the External Table and 155.12 MB for the Materialized Table

```sql
SELECT
  COUNT(DISTINCT(PULocationID))
FROM
  `tidy-arena-443619-v0.dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand`;
-- 0 MB
  
SELECT
  COUNT(DISTINCT(PULocationID))
FROM
  `tidy-arena-443619-v0.dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand_regular`;
-- 155.12 MB
```

## Question 3. Write a query to retrieve the PULocationID from the table (not the external table) in BigQuery. Now write a query to retrieve the PULocationID and DOLocationID on the same table. Why are the estimated number of Bytes different?

> BigQuery is a columnar database, and it only scans the specific columns requested in the query. Querying two columns (PULocationID, DOLocationID) requires reading more data than querying one column (PULocationID), leading to a higher estimated number of bytes processed.

```sql
SELECT
  PULocationID
FROM
  `tidy-arena-443619-v0.dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand_regular`;
-- 155.12 MB


SELECT
  PULocationID,DOLocationID
FROM
  `tidy-arena-443619-v0.dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand_regular`;
-- 310.24 MB
```


## Question 4. How many records have a fare_amount of 0??

> 8,333

```sql
SELECT
  COUNT(*)
FROM
  `tidy-arena-443619-v0.dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand`
WHERE fare_amount=0;

-- 8333
```


## Question 5. What is the best strategy to make an optimized table in Big Query if your query will always filter based on tpep_dropoff_datetime and order the results by VendorID (Create a new table with this strategy)

> Partition by tpep_dropoff_datetime and Cluster on VendorID

```sql
CREATE OR REPLACE TABLE `dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand_optimized`
PARTITION BY DATE(tpep_dropoff_datetime)
CLUSTER BY VendorID AS (
  SELECT * FROM `yellow_tripdata_simpleCommand`
);
```

## Question 6. Write a query to retrieve the distinct VendorIDs between tpep_dropoff_datetime 2024-03-01 and 2024-03-15 (inclusive)

```sql
SELECT DISTINCT(VendorID) FROM dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand_regular WHERE tpep_dropoff_datetime > '2024-03-01' AND tpep_dropoff_datetime <= '2024-03-15';
-- 310.24 MB

SELECT DISTINCT(VendorID) FROM dezoomcamp_hw3_2025.yellow_tripdata_simpleCommand_optimized WHERE tpep_dropoff_datetime > '2024-03-01' AND tpep_dropoff_datetime <= '2024-03-15';
-- 26.84 MB
```
> 310.24 MB for non-partitioned table and 26.84 MB for the partitioned table



## Question 7. Where is the data stored in the External Table you created?

> GCP Bucket


## Question 8. It is best practice in Big Query to always cluster your data

> False

## Question 9. Write a SELECT count(*) query FROM the materialized table you created. How many bytes does it estimate will be read? Why?

> 0 bytes, because it's not a expensive operation

