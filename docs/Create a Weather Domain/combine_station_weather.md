---
sidebar_position: 10
---

# Step 4: Combine the Weather & Station Data
Now that we have station data and clean weather data, we'll create the data with a Transform using Snowflake SQL. 

Create a new Transform Connector from the `CLEAN_WEATHER_DATA` Read Connector by left-selecting the vertical elipsis and selecting **Create new Transform**. 

Name the transform "WEATHER_AND_STATION" and paste the following code into the query editor:

```
SELECT 
    w.*,
    NVL(ws.name,'Unknown Station') as station_name,
    ws.latitude as station_latitude,
    ws.longitude as station_longitude
FROM 
    {{CLEAN_WEATHER_DATA}} w
    LEFT JOIN {{WEATHER_STATIONS}} ws ON w.station = CONCAT('GHCND:',ws.id)
    ```