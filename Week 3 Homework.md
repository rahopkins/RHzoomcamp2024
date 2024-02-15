## CREATE EXTERNAL TABLE
CREATE OR REPLACE EXTERNAL TABLE `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022`
OPTIONS (
    format = 'PARQUET',
    uris = ['gs://mage-zoomcamp-rh/green_taxi_2022.parquet']
);

## CHECK NEWLY CREATED TABLE
SELECT COUNT (1) FROM `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022`;
SELECT * FROM `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022` LIMIT 10;

## CREATE NON-PARTITIONED TABLE FROM EXTERNAL TABLE
CREATE OR REPLACE TABLE `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022-non-partitioned` AS
SELECT * FROM `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022`;

## HW QUESTION 1
SELECT COUNT (1) FROM `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022`;

## HW QUESTION 2
SELECT DISTINCT COUNT (pulocationid) FROM `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022`;
SELECT DISTINCT COUNT (pulocationid) FROM `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022-non-partitioned`;

## HW QUESTION 3
SELECT COUNT (*) FROM `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022`
WHERE fare_amount = 0;

## HW QUESTION 4
CREATE OR REPLACE TABLE `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022-partitioned-clustered`
PARTITION BY DATE(lpep_pickup_datetime)
CLUSTER BY pulocationid AS
SELECT * FROM `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022`;

## HW QUESTION 5
SELECT DISTINCT pulocationid from `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022-non-partitioned`
WHERE lpep_pickup_datetime between '2022-06-01 00:00:00 UTC' and '2022-06-30 23:59:59 UTC';
SELECT DISTINCT pulocationid from `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022-partitioned-clustered`
WHERE lpep_pickup_datetime between '2022-06-01 00:00:00 UTC' and '2022-06-30 23:59:59 UTC';

## HW QUESTION 8
SELECT COUNT(*) FROM `de-zoomcamp-2024-409204.ny_taxi.green-taxi-2022-non-partitioned`;
