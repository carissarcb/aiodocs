---
sidebar_position: 9
---

# Step 3: Create a WEATHER_STATIONS Read Connector
For this Read Connector, we'll use PostgreSQL Database instead of an AWS S3 bucket, so we'll need to create a PostgreSQL Connection. 

## Create a PostgreSQL Connection
On the upper left side of the screen, select **CREATE**. Then select **Read Connector** to bring up the Connectors Panel. From the Connectors Panel, select **New Connection** and you'll see a list of all possible pre-built connectors to choose from. 

Select the **PostgreSQL** connector from the Connectors Panel and enter the parameters and credentials provided by your Ascend contact. 

:::info

The PostgreSQL Connection requires parameters and credentials only accessible by an Ascend administrator. Contact your demo leader or sales representative for more information.

:::

Select **Test Connection** to confirm all settings and permissions are configured correctly.

Select **CREATE** to save this connection for future use. 

Once your connection is saved, you will see the PostgreSQL connection listed below when you choose **Read Connector** on the left panel. 

## Create a PostgreSQL Read Connector
Select  **USE** on the `ascend-postgres-gcp` Connection and select **Skip and configure manually**. Enter the following parameters:

| Field | Value | 
| --- | --- |
| Connection Name | `WEATHER_STATIONS` |
| Table Name | `ghcnd_noaa_stations` |
| Schema Name | `public` |

Select **GENERATE SCHEMA** to see a preview of the data to confirm everything looks accurate. Ascend will automatically parse the header along with the first few lines of data to generate the schema and allow you to inspect it. You can also preview the schema information to verify accuracy. 

Select **Create** once the Schema is generated.