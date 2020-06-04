---
uid: OSIsoftAdapterforBACnetPrinciplesOfOperation
---

# OSIsoft Adapter for BACnet principles of operation

This adapter's operations focus on data collection and streams creation. 

## Adapter configuration

In order for the BACnet adapter to start data collection, you need to configure the adapter by defining the following:

- Data source: Provide the data source from which the adapter should collect data.
- Data selection: Perform selection of BACnet items to which the adapter should subscribe for data.
- Logging: Set up the logging attributes to manage the adapter logging behavior.

For more information, see [OSIsoft Adapter for BACnet data source configuration](xref:OSIsoftAdapterforBACnetDataSourceConfiguration) and [OSIsoft Adapter for BACnet data selection configuration](xref:OSIsoftAdapterforBACnetDataSelectionConfiguration). 

## Connection

The BACnet adapter uses the binary bacnet.tcp protocol to communicate with the BACnet servers. When a secured connection is enabled, the X.509-type client and server certificates are exchanged and verified and the connection between the BACnet adapter and the configured BACnet server is established.

## Stream creation

The BACnet adapter creates types upon receiving the value update for a stream. One stream is created for every selected BACnet item in data selection configuration.

## Data collection

The BACnet adapter collects time-series data from selected BACnet dynamic variables through BACnet subscriptions (unsolicited reads). The adapter supports Data Access (DA) as part of the BACnet specification.

## Streams by BACnet adapter

The BACnet adapter creates a stream with two properties per selected BACnet item. The properties are described in the following table:

| Property name | Data type | Description |
|---------------|-----------|-------------|
| `Timestamp`     | DateTime  | Timestamp of the given BACnet item value update. |
| `Value`         | Specified on the type of incoming BACnet value | Value of the given BACnet item update. |

Certain metadata are sent with each stream created. Metadata common for every adapter type are

- **ComponentId**: Specifies the type of adapter, for example _BACnet_
- **ComponentType**: Specifies the data source, for example _BACnet1_

Each stream created for a given BACnet item has a unique identifier or "Stream ID." If you specify a custom stream ID for the BACnet item in data selection configuration, the adapter uses that stream ID to create the stream. Otherwise, the adapter constructs the stream ID with the following format constructed from the BACnet item node ID:

```
<Adapter Component ID>.<Namespace>.<Identifier>
```

**Note:** The naming convention is affected by `StreamPrefix` and `ApplyPrefixToStreamID` settings in data source configuration. For more information, see [OSIsoft Adapter for BACnet data source configuration](xref:OSIsoftAdapterforBACnetDataSourceConfiguration).
