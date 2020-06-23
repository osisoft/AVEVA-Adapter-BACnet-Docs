---
uid: PIAdapterforBACnetSupportedFeatures
---

# PI Adapter for BACnet supported features

This adapter provides several features including data types and exporting operation.

## Object Types and Data types
The following table lists BACnet object types that the adapter supports for data collection, stream data types and PI point types that will be created.
| BACnet object type | Stream data type | PI point type | 
|------------------|------------------|------------------|
| Accumulator       | UInt32      | Float64  |
| AnalogInput       | Single     | Float32  |
| AnalogOutput      | Single     | Float32  |
| AnalogValue       | Single     | Float32  |
| BinaryInput       | Boolean     | Int16  |
| BinaryOutput      | Boolean     | Int16  |
| BinaryValue       | Boolean     | Int16  |
| MultistateInput   | UInt32      | Float64  |
| MultistateOutput  | UInt32      | Float64  |
| MultistateValue   | UInt32      | Float64  |

## Export operation

The adapter is able to export available BACnet dynamic variables by browsing the BACnet hierarchies or sub-hierarchies.

### Export operation actions

1. To limit browsing, specify a comma-separated collection of nodeIds in data source configuration (RootNodeIds).
   
   **Note:** They are treated as roots from where the adapter starts the browse operation.
   
   The adapter triggers an export operation after a successful connection to the BACnet server when the data selection file does not exist in configuration directory.
  
2. Copy the exported data selection JSON file from the directory or retrieve it using a REST API call.

3. Optional: To avoid a potentially long and expensive browse operation, create the data selection file manually. Configure it before you configure the data source or push both in one configuration call together.
