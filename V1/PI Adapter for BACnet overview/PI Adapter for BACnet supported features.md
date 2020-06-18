---
uid: PIAdapterforBACnetSupportedFeatures
---

# PI Adapter for BACnet supported features

This adapter provides several features including data types and bitmaps.

## Object Types

The following BACnet object types are supported: 
* Accumulator
* AnalogInput
* AnalogOutput
* AnalogValue
* BinaryInput
* BinaryOutput
* BinaryValue
* MultistateInput
* MultistateOutput
* MultistateValue

## Export operation

The adapter is able to export available BACnet dynamic variables by browsing the BACnet hierarchies or sub-hierarchies.

### Export operation actions

1. To limit browsing, specify a comma-separated collection of nodeIds in data source configuration (RootNodeIds).
   
   **Note:** They are treated as roots from where the adapter starts the browse operation.
   
   The adapter triggers an export operation after a successful connection to the BACnet server when the data selection file does not exist in configuration directory.
  
2. Copy the exported data selection JSON file from the directory or retrieve it using a REST API call.

3. Optional: To avoid a potentially long and expensive browse operation, create the data selection file manually. Configure it before you configure the data source or push both in one configuration call together.
