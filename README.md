# DE-Zoomcamp-homework

##  Question 1. Understanding docker first run

Run docker with the python:3.12.8 image in an interactive mode, use the entrypoint bash.

What's the version of pip in the image?
**24.3.1**

commands:

```bash
docker build -t hw .
docker run -it hw
pip --version
```
##  Question 2. Understanding Docker networking and docker-compose

Given the following docker-compose.yaml, what is the hostname and port that pgadmin should use to connect to the postgres database?

**db:5432**

# Prepare Postgres
## Question 3. Trip Segmentation Count
During the period of October 1st 2019 (inclusive) and November 1st 2019 (exclusive), how many trips, respectively, happened:

**104,802; 198,924; 109,603; 27,678; 35,189**

```sql
-- Up to 1 mile:
SELECT COUNT(*) 
FROM public."green_taxi_Data" 
WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00' 
    AND trip_distance <= 1;

-- In between 1 (exclusive) and 3 miles (inclusive):
SELECT COUNT(*) 
FROM public."green_taxi_Data" 
WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00' 
    AND trip_distance > 1
    AND trip_distance <= 3;

-- In between 3 (exclusive) and 7 miles (inclusive):
SELECT COUNT(*) 
FROM public."green_taxi_Data" 
WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00' 
    AND trip_distance > 3
    AND trip_distance <= 7;

-- In between 7 (exclusive) and 10 miles (inclusive)
SELECT COUNT(*) 
FROM public."green_taxi_Data" 
WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00' 
    AND trip_distance > 7
    AND trip_distance <= 10;

-- Over 10 miles
SELECT COUNT(*) 
FROM public."green_taxi_Data" 
WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00' 
    AND trip_distance > 10;

```

## Question 4. Longest trip for each day
Tip: For every day, we only care about one single trip with the longest distance.

**2019-10-31**

```sql
SELECT 
    DATE(lpep_pickup_datetime),
    max(trip_distance)
FROM public."green_taxi_Data" 
WHERE DATE(lpep_pickup_datetime) IN ('2019-10-11','2019-10-24','2019-10-26','2019-10-31')
GROUP BY 1
ORDER BY 2 DESC;
```

## Question 5. Three biggest pickup zones
Which were the top pickup locations with over 13,000 in total_amount (across all trips) for 2019-10-18?

Consider only lpep_pickup_datetime when filtering by date.

East Harlem North, East Harlem South, Morningside Heights

```sql
SELECT 
    zpu."Zone",
    SUM(total_amount)
FROM public."green_taxi_Data" AS t
    LEFT JOIN public.zones zpu ON t."PULocationID"=zpu."LocationID"
WHERE DATE(lpep_pickup_datetime) = '2019-10-18'
GROUP BY 1
HAVING SUM(total_amount) > 13000
ORDER BY 2 DESC
```

## Question 6. Largest tip
For the passengers picked up in October 2019 in the zone named "East Harlem North" which was the drop off zone that had the largest tip?

Note: it's tip , not trip

We need the name of the zone, not the ID.

**JFK Airport**

```sql
SELECT "Zone" FROM public.zones 
WHERE "LocationID" IN (
    SELECT "DOLocationID"
    FROM public."green_taxi_Data" AS t
        LEFT JOIN public.zones zpu ON t."PULocationID"=zpu."LocationID"
    WHERE lpep_dropoff_datetime >= '2019-10-01 00:00:00' 
        AND lpep_dropoff_datetime < '2019-11-01 00:00:00' 
        AND zpu."LocationID"= 74 --(East Harlem North)
    GROUP BY 1
    ORDER BY max(tip_amount) DESC
    LIMIT 1)
```

# Terraform

## Question 7. Terraform Workflow

Which of the following sequences, respectively, describes the workflow for:

Downloading the provider plugins and setting up backend,
Generating proposed changes and auto-executing the plan
Remove all resources managed by terraform`

**terraform init, terraform apply -auto-approve, terraform destroy**
