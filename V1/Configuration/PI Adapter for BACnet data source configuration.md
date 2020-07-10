---
uid: PIAdapterforBACnetDataSourceConfiguration
---

# PI Adapter for BACnet data source configuration

To use the BACnet adapter, you must configure the data source to receive data.

## Configure BACnet data source

**Note:** You cannot modify BACnet data source configurations manually. You must use the REST endpoints to add or edit the configuration.

Complete the following procedure to configure the BACnet data source:

1. Using any text editor to create a file that contains a BACnet data source in JSON form.
    - For content structure, see [BACnet router data source example](#BACnet-router-data-source-example).
    - For a table of all available parameters, see [BACnet data source parameters](#BACnet-data-source-schema).
2. Save the file, for example as `DataSource.config.json`.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to execute a POST command with the contents of that file to the following endpoint: `http://localhost:<Port>/api/v1/configuration/<ComponentId>/DataSource/`. 

	**Note:** The following example uses `BACnet1` as the adapter component name. For more information on how to add a component, see [System components configuration](xref:SystemComponentsConfiguration). 

	`5590` is the default port number. If you selected a different port number, replace it with that value.

	Example using `curl`:

	**Note:** Run this command from the same directory where the file is located.

	```bash
	curl -d "@DataSource.config.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/BACnet1/DataSource"
	```

**Note:** After you complete data source configuration, the next step is to configure data selection. For more information, See [PI Adapter for BACnet data selection configuration](xref:PIAdapterforBACnetDataSelectionConfiguration).

## BACnet data source schema

The full schema definition for the BACnet data source configuration is in the `BACnet_DataSource_schema.json` file located in one of the following folders:

Windows: `%Program Files%\OSIsoft\Adapters\BACnet\Schemas`

Linux: `/opt/OSIsoft/Adapters/BACnet/Schemas`

## BACnet data source parameters

The following parameters are available to configure a BACnet data source:

| Parameter | Required | Type | Description |
|-----------|----------|------|-------------|
| **IPAddress** | Required | `string` | IPv4 address of BACnet device or BACnet router. |
| **Port**| Optional | `number` | UDP port number for communication with BACnet devices. The value ranges from `0 `to `65535`. The default port value is `47808` (the default port for the BACnet protocol).|
| **MaxConcurrentNetworkRequests** | Optional | `number` | The maximum number of requests that can be sent concurrently on the network. This is not affected by the response time for the requests. A value of `0` indicates no limit. The default is `1`.|
| **RequestDelay** | Optional | `string` | The delay between sent requests to an individual device. The value ranges from `0` to `10` seconds represented in `hh:mm:ss.fff` format. The default is `0`.|
| **AllowedConsecutiveFailedRequests** | Optional | `number` | The number of consecutive failed requests to a device before waiting for the device's **ReconnectInterval** to retry sending requests. The value ranges from `3` to `1000`. The default is `3`.|
| **ReconnectInterval** | Optional | `string` | The amount of time to wait before attempting to send requests to a device after disconnection. The value must be greater than `0` represented in `hh:mm:ss` format. The default is `1` hour or `01:00:00`.|
| **DeviceId** | Optional | `number` | Device instance number. If specified, the **IPAddress** is interpreted as for a BACnet device (not a BACnet router). If empty, the **IPAddress** is interpreted as for a BACnet router (not an individual BACnet device).|
| **NetworkNumber** | Optional | `number` | Device network number for routed BACnet devices. This setting can only be specified when a **DeviceId** is specified. If specified, the **MACAddress** must also be specified.|
| **MacAddress** | Optional | `string` | Device MAC address for routed BACnet devices. This setting can only be specified when a **DeviceId** is specified. If specified, the **NetworkNumber** must also be specified. It must contain 1-6 byte strings in hexadecimal format, separated by a dash `-` or colon `:` (for example, `12:34:ef:cd`). |
| **StreamIdPrefix** | Optional | `string` | Specifies what prefix is used for stream IDs. The naming convention is `StreamIdPrefix.StreamId`. An empty string means no prefix will be added to the stream IDs and names. A `null` value defaults to _ComponentID_ followed by a period (for example, `BACnet1.NamespaceIndex.Identifier.`).<br><br>**Note:** If you change the **StreamIdPrefix** of a configured adapter, for example when you delete and add a data source, you need to restart the adapter for the changes to apply. New streams are created on adapter restart and pre-existing streams no longer update. |
| **DefaultStreamIdPattern** | Optional | `string` | Specifies the default stream ID pattern to use. Possible parameters: {**DeviceIPAddress**}, {**DeviceId**}, {**ObjectType**}, {**ObjectId**}, and {**PropertyIdentifier**}. An empty or `null` value will result in {**DeviceId**}.{**ObjectType**}{**ObjectId**}.{**PropertyIdentifier**}`.|


## BACnet router data source example

The following is an example of valid BACnet data source configuration:

```json
{
	"IPAddress": "192.168.1.1",
	"Port": 47808,
	"MaxConcurrentNetworkRequests" : 0,
	"RequestDelay": "00:00:00",
	"AllowedConsecutiveFailedRequests": 3,
	"ReconnectInterval": "02:00:00"
}
```

## BACnet routed device data source example

The following is an example of valid BACnet routed device data source configuration:

```json
{
    "IPAddress": "192.168.1.1",
	"Port": 47808,
	"MaxConcurrentNetworkRequests" : 1,
	"RequestDelay": "00:00:00",
	"AllowedConsecutiveFailedRequests": 3,
	"ReconnectInterval": "02:00:00",
	"DeviceID": 1,
	"NetworkNumber": 100,
	"MacAddress": "12"
}
```
## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/_ComponentId_/DataSource | `GET` | Retrieves the BACnet data source configuration |
| api/v1/configuration/_ComponentId_/DataSource  | `POST` | Creates the BACnet data source configuration |
| api/v1/configuration/_ComponentId_/DataSource | `PUT` | Configures or updates the BACnet data source configuration |
| api/v1/configuration/_ComponentId_/DataSource | `DELETE` | Deletes the BACnet data source configuration |

**Note:** Replace _ComponentId_ with the Id of your BACnet component. For example, `BACnet1`.

## Discovery
The BACnet adapter is able to discover available BACnet devices and objects defined by the data source configuration. In the case of discovery for a BACnet router, the adapter sends a *Who-Is* request and waits 30 seconds to receive *I-Am* responses from available devices. Upon receiving an *I-Am* response, the adapter requests the *Protocol Services Supported*, *Maximum APDU Length*, *Segmentation* and *Object List* properties from the available devices. In the case of discovering a single device, the adapter will not send a *Who-Is* request but instead request properties. 

A successful discovery results in populating [DeviceConfiguration](xref:PIAdapterforBACnetDataSelectionConfiguration#BACnet-device-configuration) and optionally, [DataSelection Configuration](xref:PIAdapterforBACnetDataSelectionConfiguration#Configure-BACnet-data-selection).
* DataSelection will be populated with *Selected* attribute for all items set to `false`. 
* DeviceConfiguration is read-only and provides more information such as segmentation and services that are supported. This cam help make informed decisions in data selection. 

When the adapter starts or a new data source is configured, the adapter checks if DeviceConfiguration is populated. Discovery is performed only if DeviceConfiguration is empty. DataSelection will update by discovery only if it is empty.

The adapter [log](xref:Logging-configuration) indicates when discovery is complete.

### Example log

[15:17:49 INF] [Bacnet] Discovering BACnet router.  
[15:18:19 INF] [Bacnet] Found 2 BACnet devices during discovery.   
[15:18:19 INF] [Bacnet] Discovering BACnet device 1.  
[15:18:21 INF] [Bacnet] Discovery complete for BACnet device 1.  
[15:18:21 INF] [Bacnet] Discovering BACnet device 33.  
[15:18:53 INF] [Bacnet] Discovery complete for BACnet router.  
