---
sidebar_position: 15
---

# Step 3: Create a Final Data Product
The final three data products are created using Transforms.

## Create a Bad Weather Rides Transform
Create a new Transform Connector from the `Weather and Rides` Transform by left-selecting the vertical elipsis and selecting **Create new Transform**. 

Name the transform "Bad Weather Rides" and paste the following code into the query editor:

```
SELECT * FROM {{Weather_and_Rides}} AS w
WHERE w.WEATHER NOT IN('Not Rainy')
```

## Create an All Rides with Weather Transform
Create a new Transform Connector from the `Weather and Rides` Transform by left-selecting the vertical elipsis and selecting **Create new Transform**. 

Name the transform "All Rides with Weather" and paste the following code into the query editor.

```
SELECT * FROM {{Weather_and_Rides}} AS w
```

## Create a Good Weather Rides Transform
Create a new Transform Connector from the `Weather and Rides` Transform by left-selecting the vertical elipsis and selecting **Create new Transform**. 

Name the transform "Good Weather Rides" and paste the following code into the query editor.

```
SELECT * FROM {{Weather_and_Rides}} AS w
WHERE w.WEATHER = 'Not Rainy'
```


Your completed Data Mesh Product should look like this:
