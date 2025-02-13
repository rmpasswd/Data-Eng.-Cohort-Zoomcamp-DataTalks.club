## Homework: Week 03

- BIG QUERY SETUP:  Create an external table using the Yellow Taxi Trip Records.
    ```
    CREATE OR REPLACE EXTERNAL TABLE `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_external` 
    OPTIONS (
      format = 'parquet',
      uris = ['gs://new_york_tlc_yellow_trips_2024_jan_jun/*.parquet']
    )```


- BIG QUERY SETUP:  Create a (regular/materialized) table in BQ using the Yellow Taxi Trip Records (do not partition or cluster this table)
     ```
    CREATE OR REPLACE TABLE `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_regular` 
    as (
      SELECT * FROM `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_external`
    );
     ```

- Question 1: What is count of records for the 2024 Yellow Taxi Data?  
    ```
  SELECT COUNT(*) FROM  `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_regular`;
 

- Question 2. Estimated amount of data (1 point)  
   ```
     SELECT COUNT(DISTINCT PULocationID) FROM  `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_regular`; - 155MB  
    SELECT COUNT(DISTINCT PULocationID) FROM  `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_external`; - 0B

- Question 3. Why are the estimated number of Bytes different? (1 point)  
    ```
  SELECT  PULocationID FROM  `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_regular`; - 155MB  
    SELECT  PULocationID, DOLocationID FROM  `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_regular`; - 310MB

- Question 4. How many records have a fare_amount of 0? (1 point)  
    ```
  SELECT  COUNT(*)   FROM  `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_regular` WHERE fare_amount=0; - 155MB



- Question 5: Make an optimized table in Big Query if your query will always filter based on tpep_dropoff_datetime and order the results by VendorID 
   ```
   CREATE OR REPLACE TABLE `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_part`
    PARTITION BY DATE(`tpep_pickup_datetime`)
    CLUSTER BY `VendorID`
    AS (  
    SELECT * FROM `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_regular` 
    )
 
- Question 6: Write a query to retrieve the distinct VendorIDs between tpep_dropoff_datetime 2024-03-01 and 2024-03-15 (inclusive)
  
    ```
  SELECT distinct VendorID FROM `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_part`  WHERE `tpep_dropoff_datetime` BETWEEN "2024-03-01" AND "2024-03-15"; - 26.84 MB  
    SELECT distinct VendorID FROM `data-eng-450213.ny_taxi_2024.yellow_2024_jan_jun_regular`  WHERE `tpep_dropoff_datetime` BETWEEN "2024-03-01" AND "2024-03-15"; - 310.24 MB


 
