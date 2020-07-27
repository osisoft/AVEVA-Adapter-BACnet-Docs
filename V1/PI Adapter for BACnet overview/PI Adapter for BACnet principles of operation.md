---
uid: PIAdapterforBACnetPrinciplesOfOperation
---

# PI Adapter for BACnet principles of operation

The BACnet adapter's operations focus on data collection and streams creation.

## Adapter configuration

For the BACnet adapter to start data collection, you need to configure the adapter by defining the following:

- Data source: Provide the data source from which the adapter should collect data.
- Data selection: Select BACnet items to which the adapter should request data or subscribe for data.
- Logging: Set up the logging attributes to manage the adapter logging behavior.

For more information, see [PI Adapter for BACnet data source configuration](xref:PIAdapterforBACnetDataSourceConfiguration), [PI Adapter for BACnet data selection configuration](xref:PIAdapterforBACnetDataSelectionConfiguration), and [Logging configuration](xref:LoggingConfiguration).

## Data collection

The BACnet adapter collects time-series data from selected objects on BACnet devices. The adapter supports both polling and COV (Change of Value, unsolicited subscription) data collection modes, as defined by the BACnet specification.

### Object types and data types

The following table lists BACnet object types that the BACnet adapter supports for data collection and types of streams that will be created.

| BACnet object type | Stream data type |
|------------------|------------------|
| Accumulator       | `UInt32`  |
| AnalogInput       | `Single`  |
| AnalogOutput      | `Single`  |
| AnalogValue       | `Single`  |
| BinaryInput       | `Boolean` |
| BinaryOutput      | `Boolean` |
| BinaryValue       | `Boolean` |
| MultistateInput   | `UInt32`  |
| MultistateOutput  | `UInt32`  |
| MultistateValue   | `UInt32`  |

## Stream creation

The BACnet adapter creates a stream with two properties for a selected BACnet item. The properties are described in the following table:

| Property name | Data type | Description |
|---------------|-----------|-------------|
| `Timestamp`     | DateTime  | Timestamp of the given BACnet item value update. |
| `Value`         | Specified on the type of incoming BACnet value | Value of the BACnet item update. |

**Note:** If streams are deleted from an endpoint while the adapter is running, the adapter process must be restarted in order for the streams to be recreated.

Certain metadata are sent with each stream created.
The following metadata are common for every adapter type:

- **ComponentId**: Specifies the data source, for example, _BACnet1_ 
- **ComponentType**: Specifies the type of adapter, for example, _BACnet_

Metadata specific to the BACnet adapter:

- **Device**: The Device ID of the BACnet device
- **SourceId**: SourceId is constructed using the following pattern: {DeviceId}.{ObjectType}{ObjectId}.{PropertyIdentifier}
- **LocalName**: The BACnet ObjectName as provided by the BACnet object

The metadata level is set in [General configuration](xref:GeneralConfiguration). For the BAcnet adapter, the following metadata is sent for the individual level:

- `None`: No metadata
- `Low`: AdapterType (_ComponentType_) and DataSource (_ComponentId_)
- `Medium`: AdapterType (_ComponentType_), DataSource (_ComponentId_), and Schedule (ScheduleId)
- `High`: AdapterType (ComponentType), DataSource (ComponentId), Schedule (ScheduleId), Device, SourceId and LocalName

**Note:** If a `ScheduleId` is not specified when configuring data selection items (see [PI Adapter for BACnet data selection configuration](xref:PIAdapterforBACnetDataSelectionConfiguration)), metadata will not be sent for the associated streams until the `ScheduleId` is specified and the adapter process is restarted.

Each stream created for a given BACnet item has a unique identifier (stream ID). If you specify a custom stream ID for the BACnet item in data selection configuration, the adapter uses that stream ID to create the stream. Otherwise, the adapter constructs the stream ID with the following format constructed from the BACnet item node ID:

```code
<Adapter Component ID>.<Device ID>.<Object Type><Object ID>.<Property Identifier>
```

**Note:** The naming convention is affected by `StreamIdPrefix` and `DefaultStreamIdPattern` settings in data source configuration. For more information, see [PI Adapter for BACnet data source configuration](xref:PIAdapterforBACnetDataSourceConfiguration).
