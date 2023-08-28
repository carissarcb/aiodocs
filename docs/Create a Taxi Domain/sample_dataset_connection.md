---
sidebar_position: 2
---

# Creating Taxi Read Connectors
The first step for creating a data product is creating Connections and Read Connectors that access the weather and taxi cab data from AWS S3. 

## Create a **Sample Datasets** Connection
On the upper left side of the screen, select **CREATE**. Then select **Read Connector** to bring up the Connectors Panel. From the Connectors Panel, select **New Connection** and you'll see a list of all possible pre-built connectors to choose from. 

For today's lab, we're connecting to an AWS S3 source. Select the **Amazon S3** connector from the Connectors Panel and enter the following parameters:

| Field | Value | 
| --- | --- |
| Access Type | Read-Only |
| Connection Name | `Sample Datasets` |
| Connection Type | `ascend-io-sample-data-read` |
| Requires Credentials | Leave unchecked. The data we are using does not require credentials. |

Select **Test Connection** to confirm all S3 bucket settings and permissions are configured correctly.

Select **CREATE** to save this connection for future use. 

Once your connection is saved, you will see the S3 connection listed below when you choose **Read Connector** on the left panel.

## Create a GREEN_CABS Read Connector
Select  **USE** on the Sample Datasets S3 Read Connector and select **Skip and configure manually**. Enter the following parameters:

| Field | Value | 
| --- | --- |
| Connection Name | `GREEN_CABS` |
| Object Pattern Matching | Regex |
| Object Pattern | `NYC-TAXI/green_cab/2016-0[1-3]/.*.csv` |
| Parser | CSV |
| Fields Have a Header Row | Check this box. |

Select **GENERATE SCHEMA** to see a preview of the CSV to confirm everything looks accurate. Ascend will automatically parse the header along with the first few lines of data to generate the schema and allow you to inspect it. You can also preview the schema information to verify accuracy.

## Create a YELLOW_CABS Read Connector
Repeat the same steps for the `GREEN_CABS` read connector with the following parameters:

| Field | Value | 
| --- | --- |
| Connection Name | `YELLOW_CABS` |
| Object Pattern Matching | Glob |
| Object Pattern | `NYC-TAXI/yellow_cab/2016-01/*` |
| Parser | CSV |
| Fields Have a Header Row | Check this box. |

Don't forget to **Generate Schema** before selecting **CREATE**!