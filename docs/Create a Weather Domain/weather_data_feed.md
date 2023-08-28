---
sidebar_position: 11
---

# Step 5: Creating Data Feed Connectors
The final step in our Weather Domain is to create a Data Feed. 

## Create a MESH_DOMAIN_TAXI_DATA Data Feed
From the `CLEAN_WEATHER_DATA` Transform, right-select the vertical elipsis and select **Create New Data Feed**. 

Name the Data Feed `MESH_DOMAIN_WEATHER`. Ensure the **Upstream** field is set to `WEATHER_AND_STATION`. For **Permission Settings**, select "**All teams in all Data Services...**."

Your completed Weather Domain should look like this: