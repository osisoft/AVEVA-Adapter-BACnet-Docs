---
uid: OSIsoftAdapterforBACnetDataSourceConfiguration
---

# OSIsoft Adapter for BACnet data source configuration

To use the BACnet adapter, you must configure the data source from which it will be receiving data.

## Configure BACnet data source

**Note:** You cannot modify BACnet data source configurations manually. You must use the REST endpoints to add or edit the configuration.

Complete the following procedure to configure the BACnet data source:

1. Using any text editor, create a file that contains a BACnet data source in JSON form.
    - For content structure, see [BACnet data source example](#BACnet-data-source-example).
    - For a table of all available parameters, see [BACnet data source parameters](#BACnet-data-source-schema).
2. Save the file, for example as _DataSource.config.json_.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to execute a POST command with the contents of that file to the following endpoint: `http://localhost:<Port>/api/v1/configuration/<adapterId>/DataSource/`. 

**Note:** The following example uses BACnet1 as the adapter component name. For more information on how to add a component, see System components configuration. 5590 is the default port number. If you selected a different port number, replace it with that value.

```bash
curl -v -d "@DataSource.config.json" -H "Content-Type: application/json" "http://localhost:5590/api/v1/configuration/BACnet1/DataSource"
```

**Note:** After you have completed data source configuration, the next step is to configure data selection. For more information, See [OSIsoft Adapter for BACnet data selection configuration](xref:OSIsoftAdapterforBACnetDataSelectionConfiguration).

## BACnet data source schema

The full schema definition for the BACnet data source configuration is in the _BACnet_DataSource_schema.json_ here:

Windows: *%Program Files%\OSIsoft\Adapters\BACnet\Schemas*

Linux: */opt/OSIsoft/Adapters/BACnet/Schemas*

## BACnet data source parameters

The following parameters can be used to configure an BACnet data source:

| Parameter | Required | Type | Nullable | Description |
|-----------|----------|------|----------|-------------|
| **IPAddress** | Required | `string` | Yes | IPv4 address of BACnet device or BACnet Router|
| **Port**|Optional | `number` | No | UDP port number for communication with BACnet devices. The value ranges from 0 to 65535. If not configured, the default port is 47808 (which is the default port for BACnet protocol).|
| **MaxConcurrentNetworkRequests** | Optional | `number` | No | The maximum number of requests that can be sent concurrently on the network. This is not affected by the response time for the requests. The value must be greater than 0. The default is 1.|
| **DeviceRequestDelay** | Optional | `number` | No | The delay in milliseconds between sending requests to an individual device. The value ranges from 0 to 10000 milliseconds. The default is 0 ms.|
| **AllowedConsecutiveFailedRequests** | Optional | `number` | No | The number of consecutive failed requests to a device before setting the device status to disconnected and waiting DeviceReconnectInterval to try sending requests again. The value ranges from 3 to 1000. The default is 3.|
| **DeviceReconnectInterval** | Optional | `number` | No | The amount of time in minutes to wait before attempting to send requests to a device after it has disconnected. The value must be greater than 0. The default is 60 minutes.|
| **DeviceId** | Optional | `number` | yes | Device instance number. If specified, indicates IPAddress is for a BACnet device (not a BACnet router). If empty, indicates the IPAddress is for a BACnet router (not an individual BACnet device).|
| **NetworkNumber** | Optional | `number` | Yes | Device network number for routed BACnet devices. This setting must be used in tandem with DeviceId and MACAddress.|
| **MacAddress** | Optional | `string` | Yes | Device MAC address for routed BACnet devices. This setting must be used in tandem with DeviceId and NetworkNumber.|
| **StreamPrefix** | Optional | `string` | Yes | Specifies what prefix is used for Stream IDs and names. **Note:** An empty string means no prefix will be added to the Stream IDs and names. Null value means ComponentID followed by dot character will be added to the stream IDs and names. |
| **ApplyPrefixToStreamId** | Optional | `boolean` | No | Parameter applied to all data items collected from the data source that have custom stream ID configured. If configured, the adapter will apply the StreamIdPrefix property to all the streams with custom ID configured. The property does not affect any streams with default ID configured|


## BACnet data source example

The following is an example of valid BACnet data source configuration:

```json
{
	"IPAddress": "192.168.1.1",
	"Port": 47808,
	"MaxConcurrentNetworkRequests" : 5,
	"DeviceRequestDelay": 10,
	"AllowedConsecutiveFailedRequests": 3,
	"DeviceReconnectInterval": 120
}
```

## Routed BACnet device data source example

The following is an example of valid routed BACnet data source configuration:

```json

{
    "IPAddress": "192.168.1.1",
	"Port": 47808,
	"MaxConcurrentNetworkRequests" : 5,
	"DeviceRequestDelay": 10,
	"AllowedConsecutiveFailedRequests": 3,
	"DeviceReconnectInterval": 120,
	"DeviceID": 1,
	"NetworkNumber": 100,
	"MacAddress": "12"
}
```
