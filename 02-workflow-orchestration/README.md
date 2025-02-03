# DE-Zoomcamp-homework

##  Question 1. Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file yellow_tripdata_2020-12.csv of the extract task)?

> **134.5 MB**

##  Question 2. What is the rendered value of the variable file when the inputs taxi is set to green, year is set to 2020, and month is set to 04 during execution?

> **green_tripdata_2020-04.csv**

## Question 3. How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?

> **24,648,499**

```sql
SELECT 
( (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_01`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_02`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_03`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_04`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_05`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_06`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_07`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_08`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_09`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_10`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_11`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.yellow_tripdata_2020_12`)) 
```



## Question 4. How many rows are there for the Green Taxi data for all CSV files in the year 2020?

> **1,734,051**

```sql
SELECT 
( (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_01`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_02`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_03`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_04`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_05`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_06`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_07`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_08`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_09`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_10`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_11`) 
+ (SELECT COUNT(*) FROM `tidy-arena-443619-v0.zoomcamp.green_tripdata_2020_12`)) 
```


## Question 5. How many rows are there for the Yellow Taxi data for the March 2021 CSV file?

> **1,925,152**


## Question 6. How would you configure the timezone to New York in a Schedule trigger?
https://kestra.io/docs/workflow-components/triggers/schedule-trigger

> **Add a timezone property set to America/New_York in the Schedule trigger configuration**
