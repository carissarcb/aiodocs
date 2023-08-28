---
sidebar_position: 14
---

# Step 2: Filter and Join Weather and Taxi Data
Next we'll work with the data from the weather domain and prepare it for joining with the taxi domain.

## Create a UNIQUE WEATHER BY DAY Transform
Create a new Transform Connector from the `MESH_DOMAIN_WEATHER` Data Feed by left-selecting the vertical elipsis and selecting **Create new Transform**. 

Name the transform "UNIQUE WEATHER BY DAY" and paste the following code into the query editor:

```
SELECT 
    WEATHER_DATE,
    DATATYPE,
    STATION,
    WEATHER,
    PRECIPITATION,
    STATION_NAME
     from (
        select *, row_number() over (
            partition by WEATHER_DATE
            order by STATION_NAME desc
        ) as row_num
        from {{MESH_DOMAIN_WEATHER}}
    ) as ordered_weather
WHERE ordered_weather.row_num = 1
```

## Create a Weather and Rides Transform
Create a new Transform Connector from the `UNIQUE WEATHER BY DAY` Transform by left-selecting the vertical elipsis and selecting **Create new Transform**. 

Name the transform "Weather and Rides" and paste the following code into the query editor.

```
SELECT 
T.*, 
W.WEATHER
FROM {{MESH_DOMAIN_TAXI_DATA}} T
LEFT JOIN {{UNIQUE_WEATHER_BY_DAY}} W ON W.WEATHER_DATE = T.RIDE_DATE
```