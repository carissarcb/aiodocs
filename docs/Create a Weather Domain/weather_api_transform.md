---
sidebar_position: 8
---

# Step 2: Create Relational & Clean Transforms

## Create a Relational Weather Data Transform
Create a new Transform Connector from the `WEATHER_API_RAW` Read Connector by left-selecting the vertical elipsis and selecting **Create new Transform**. 

Name the transform "RELATIONAL_WEATHER_DATA" and paste the following code into the query editor:

```
 SELECT
  TO_DATE(GET(w.PARSED, 'date')) as DATE,
  GET(w.PARSED, 'datatype') as DATATYPE, 
  GET(w.PARSED, 'station') as STATION,
  TO_DECIMAL(GET(w.PARSED, 'value')) as VALUE,
  'weather' as WEATHER_TYPE
FROM
  (SELECT PARSE_JSON(w.HTTP_RESPONSE) as PARSED FROM {{WEATHER_API_RAW}} AS w) AS w
  ```

## Create a CLEAN_WEATHER_DATA Transform
Create another transform for the `RELATIONAL_WEATHER_DATA` Transform to clean the data. 

Name the Transform "CLEAN_WEATHER_DATA" and paste the following code into the query editor:

```
SELECT 
  ADD_MONTHS(DATEADD(day, UNIFORM(0,31, RANDOM()), w.DATE), -48) as WEATHER_DATE,
  w.DATATYPE,
  w.STATION,
  CASE
    WHEN SUM(w.VALUE) >= 2.5 THEN 'Rainy'
    ELSE 'Not Rainy'
  END as WEATHER,
  SUM(w.value) as PRECIPITATION
FROM
  {{RELATIONAL_WEATHER_DATA}} AS w
WHERE
  w.DATATYPE = 'PRCP'
GROUP BY
  w.DATATYPE,
  w.STATION,
  WEATHER_DATE
  ```