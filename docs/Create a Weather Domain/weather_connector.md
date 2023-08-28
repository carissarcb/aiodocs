---
sidebar_position: 6
---

# Step 1: Create a WEATHER_API_RAW Read Connector
For the Weather Domain, we'll skip creating a new **Connection** since Connections are accessible throughout the Data Service.

Select  **USE** on the Sample Datasets S3 Connection and select **Skip and configure manually**. Enter the following parameters:

| Field | Value | 
| --- | --- |
| Connection Name | `WEATHER_API_RAW` |
| Object Pattern Matching | Match |
| Object Pattern | `weather/api_data.csv` |
| Parser | CSV |
| Fields Have a Header Row | Check this box. |

Select **GENERATE SCHEMA** to see a preview of the CSV to confirm everything looks accurate. Ascend will automatically parse the header along with the first few lines of data to generate the schema and allow you to inspect it. You can also preview the schema information to verify accuracy.