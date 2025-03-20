# DE-Zoomcamp-homework

##  Question 1: Install Spark and PySpark
> '3.3.2'

```python
spark.version
```

##  Question 2: Yellow October 2024
> 25MB
```python
df = df.repartition(4)
df.write.parquet('hm')
```

## Question 3: Count records
> 128893
```python
spark.sql("""
SELECT
    COUNT(1)
FROM 
    hm
WHERE
    to_date(tpep_pickup_datetime) = '2024-10-15';
""").show()
```


## Question 4: Longest trip
> 162.6177777777778
```python
spark.sql("""
SELECT
    MAX((CAST(tpep_dropoff_datetime AS LONG) - CAST(tpep_pickup_datetime AS LONG)) / 60 / 60) AS duration
FROM 
    hm;
""").show()
```


## Question 5: User Interface

> 4040

## Question 6: Least frequent pickup location zone
> Governor's Island...

```python
spark.sql("""
SELECT
    Zone,
    LocationID,
    INT(COUNT(PULocationID))
FROM 
    hm LEFT JOIN zones ON hm.PULocationID=zones.LocationID
GROUP BY 1,2
ORDER BY 3;
""").show()
```