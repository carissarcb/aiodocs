---
sidebar_position: 3
---

# Creating Taxi Transforms
After creating read connectors, we'll create a Transform using Snowflake SQL. 

## Create a ALL_CAB_DATA Transform
Create a new Transform Connector by From the `YELLOW_CABS` transform, left-select the vertical elipsis and select **Create new Transform**. Alternatively, select **Snowflake SQL** from the Transform menu located in the toolbox.

Name the transform "ALL_CAB_DATA" and paste the following code into the query editor.

```
SELECT
VendorID as vendor_id,
lpep_pickup_datetime as pickup_datetime,
TO_TIMESTAMP(Lpep_dropoff_datetime) as dropoff_datetime,
RateCodeID as rate_code_id,
Pickup_longitude as pickup_lon,
Pickup_latitude as pickup_lat,
Dropoff_longitude as dropoff_lon,
Dropoff_latitude as dropoff_lat,
Passenger_count as passenger_count,
Trip_distance as distance,
Fare_amount as amount_fare,
Extra as amount_extra,
MTA_tax as amount_tax,
Tip_amount as amount_tip,
Tolls_amount as amount_tolls,
IFNULL(TRY_TO_DECIMAL(Ehail_fee,10,2),TO_DECIMAL(0.0,10,2)) as amount_hail_fee,
improvement_surcharge as amount_surcharge,
Total_amount as amount_total,
Payment_type as payment_type,
Trip_type as trip_type,
'green' as cab_color
FROM {{GREEN_CABS}}

UNION ALL

SELECT
VendorID as vendor_id,
tpep_pickup_datetime as pickup_datetime,
TO_TIMESTAMP(tpep_dropoff_datetime) as dropoff_datetime,
RatecodeID as rate_code_id,
pickup_longitude as pickup_lon,
pickup_latitude as pickup_lat,
dropoff_longitude as dropoff_lon,
dropoff_latitude as dropoff_lat,
passenger_count as passenger_count,
trip_distance as distance,
fare_amount as amount_fare,
extra as amount_extra,
mta_tax as amount_tax,
tip_amount as amount_tip,
tolls_amount as amount_tolls,
TO_DECIMAL(0.0, 10, 2) as amount_hail_fee,
improvement_surcharge as amount_surcharge,
Total_amount as amount_total,
payment_type as payment_type,
-1 as trip_type,
'yellow' as cab_color
FROM {{YELLOW_CABS}}
```

Set **Component Pausing** to **Running** and leave **Advanced Settings** unconfigured.

Select **CREATE** and Ascend will begin processing your SQL query immediately. 

## Create CONTROL_CAB_DATA Transform
From the `ALL_CAB_DATA` transform, left-select the vertical ellipsis and select **Create new Transform**. 

Name the transform `CONTROL_CAB_DATA` and paste the following code in the query editor:

```
SELECT *,
TO_DATE(p.PICKUP_DATETIME) AS RIDE_DATE, 'new' as jto_col
FROM {{PARTITION_CAB_DATA_2}} AS p
```