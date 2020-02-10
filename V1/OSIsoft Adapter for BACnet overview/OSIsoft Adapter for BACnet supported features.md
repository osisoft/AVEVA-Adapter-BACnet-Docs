---
uid: OSIsoftAdapterforBACnetSupportedFeatures
---

# OSIsoft Adapter for BACnet supported features

This adapter provides several features including data types and bitmaps.

## Data types

The following table lists BACnet variable types that the adapter supports data collection from and types of streams that are going to be created.

| BACnet data type | Stream data type |
|------------------|------------------|
| Boolean          | Boolean          |
| Byte             | Int16            |
| SByte            | Int16            |
| Int16            | Int16            |
| UInt16           | UInt16           |
| Int32            | Int32            |
| UInt32           | UInt32           |
| Int64            | Int64            |
| UInt64           | UInt64           |
| Float            | Float32          |
| Double           | Float64          |
| DateTime         | DateTime         |
| String           | String           |

## Export operation


The adapter is able to export available BACnet dynamic variables by browsing the BACnet hierarchies or sub-hierarchies.

### Export operation actions

1. To limit browsing, specify a comma-separated collection of nodeIds in data source configuration (RootNodeIds).
   
   **Note:** They are treated as roots from where the adapter starts the browse operation.
   
   The adapter triggers an export operation after a successful connection to the BACnet server when the data selection file does not exist in configuration directory.
  
2. Copy the exported data selection JSON file from the directory or retrieve it using a REST API call.

3. Optional: To avoid a potentially long and expensive browse operation, create the data selection file manually. Configure it before you configure the data source or push both in one configuration call together.
