---
uid: PIAdapterforBACnetDataSourceConfiguration
---

# Data source configuration

To use the BACnet adapter, you must configure the data source to receive data.

**Note:** This procedure uses cURL commands for REST endpoint configuration, but other options are available. For more information, see [Configuration tools](xref:ConfigurationTools).

## To configure the data source

Complete the following steps to configure the BACnet data source. Use the `PUT` method in conjunction with the following endpoint to initialize the configuration: `api/v1/configuration/<ComponentId>/DataSource`.

1. Using a text editor, create an empty text file.

1. Copy and paste an example configuration for a BACnet router or routed device into the file.

    [Data source examples](#data-source-examples)

1. Update the example JSON parameters for your environment.

    [Data source parameters](#data-source-parameters)

1. Save the file as `ConfigureDataSource.json`.

1. Open a command line session. Change directory to the location of `ConfigureDataSource.json`.

1. Enter the following cURL command (which uses the `PUT` method) to initialize the BACnet data source configuration.

    ```bash
    curl -d "@ConfigureDataSource.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/BACnet1/DataSource"
    ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number in use.
    * If using a component ID other than `BACnet1`, update the endpoint with your chosen component ID.
    * For a list of other REST operations you can perform, like updating or deleting a data source, see [REST URLs](#rest-urls).
    <br/>
    <br/>

1. Configure data selection. For more information, see [PI Adapter for BACnet data selection configuration](xref:PIAdapterforBACnetDataSelectionConfiguration).

## Data source schema

The full schema definition for the BACnet data source configuration is in the `BACnet_DataSource_schema.json` file located in one of the following folders:

* Windows: `%Program Files%\OSIsoft\Adapters\BACnet\Schemas`
* Linux: `/opt/OSIsoft/Adapters/BACnet/Schemas`

## Data source parameters

The following parameters are available to configure a BACnet data source:

| Parameter | Required | Type | Description |
|-----------|----------|------|-------------|
| **IPAddress** | Required | `string` | IPv4 address of BACnet device or BACnet router. |
| **Port**| Optional | `number` | UDP port number for communication with BACnet devices.<br><br>Value range: `0` to `65535`<br>Default value: `47808` (the default port for the BACnet protocol)|
| **MaxConcurrentNetworkRequests** | Optional | `number` | The maximum number of requests that can be sent concurrently on the network. This is not affected by the response time for the requests. A value of `0` indicates no limit.<br><br>Default value: `1`
| **RequestDelay** | Optional | `string` | The delay between sent requests to an individual device represented in `hh:mm:ss.fff` format.<br><br>Minimum value: `00:00:00.000` for `0` seconds<br>Maximum value: `00:00:10.000` for `10` seconds<br> Default value: `00:00:00.000`|
| **AllowedConsecutiveFailedRequests** | Optional | `number` | The number of consecutive failed requests to a device before waiting **ReconnectInterval** to retry sending requests.<br><br>Minimum value: `3`<br>Maximum value: `1000`<br>Default value: `3`|
| **ReconnectInterval** | Optional | `string` | The amount of time to wait before attempting to send requests to a device after disconnection represented in `hh:mm:ss` format.<br><br>Allowed value: Must be greater than `0`<br>Default value: `01:00:00` for `1` hour|
| **DeviceId** | Optional | `number` | Device instance number. If specified, the **IPAddress** is interpreted as for a BACnet device (not a BACnet router). If empty, the **IPAddress** is interpreted as for a BACnet router (not an individual BACnet device).|
| **NetworkNumber** | Optional | `number` | Device network number for routed BACnet devices. This setting can only be specified when a **DeviceId** is specified. If specified, the **MACAddress** must also be specified.|
| **MacAddress** | Optional | `string` | Device MAC address for routed BACnet devices. This setting can only be specified when a **DeviceId** is specified. If specified, the **NetworkNumber** must also be specified. It must contain 1-6 byte strings in hexadecimal format, separated by a dash `-` or colon `:`<br><br>Example: `12:34:ef:cd` |
| **StreamIdPrefix** | Optional | `string` | Specifies what prefix is used for stream IDs. The naming convention is `{StreamIdPrefix}{StreamId}`. An empty string means no prefix will be added to the stream IDs and names. A `null` value defaults to **ComponentID** followed by a period.<br><br>Example: `BACnet1.{DeviceId}.{ObjectType}{ObjectId}.{PropertyIdentifier}`<br><br>**Note:** If you change the **StreamIdPrefix** of a configured adapter, for example when you delete and add a data source, you need to restart the adapter for the changes to take place. New streams are created on adapter restart and pre-existing streams are no longer updated.<br><br>Allowed value: any string<br>Default value: `null`|
| **DefaultStreamIdPattern** | Optional | `string` | Specifies the default stream ID pattern to use. Possible parameters: `{DeviceIPAddress}`, `{DeviceId}`, `{ObjectType}`, `{ObjectId}`, and `{PropertyIdentifier}`.<br><br>Allowed value: any string<br>Default value: `{DeviceId}.{ObjectType}{ObjectId}.{PropertyIdentifier}` |

## Data source examples

Use one of the following examples as a template for your BACnet data source configuration.

### BACnet router data source example

The following is an example of a valid BACnet data source configuration:

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

### BACnet routed device data source example

The following is an example of a valid BACnet routed device data source configuration:

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
| api/v1/configuration/\<ComponentId\>/DataSource | `GET` | Retrieves the data source configuration. |
| api/v1/configuration/\<ComponentId\>/DataSource | `POST` | Creates the data source configuration. The adapter starts collecting data after the following conditions are met:<br/><br/>&bull; The data source configuration `POST` request is received.<br/>&bull; A data selection configuration is active. |
| api/v1/configuration/\<ComponentId\>/DataSource | `PUT` | Configures or updates the data source configuration. Overwrites any active data source configuration. If no configuration is active, the adapter starts collecting data after the following conditions are met:<br/><br/>&bull; The data source configuration `PUT` request is received.<br/>&bull; A data selection configuration is active. |
| api/v1/configuration/\<ComponentId\>/DataSource | `DELETE` | Deletes the data source configuration. After the request is received, the adapter stops collecting data. |

**Note:** Replace \<ComponentId\> with the Id of your BACnet component. For example, BACnet1.

## Discovery

The adapter is able to discover available BACnet devices and objects defined by the data source configuration. For discovery of a BACnet router, the adapter sends a *Who-Is* request and waits 30 seconds to receive *I-Am* responses from available devices. Upon receiving an *I-Am* response, the adapter requests the *Protocol Services Supported*, *Maximum APDU Length*, *Segmentation* and *Object List* properties from the available devices. For discovery of a single device, the adapter does not send a *Who-Is* request but proceeds to request its properties.

When the adapter starts or a new data source is configured, the adapter checks if device configuration is populated. Discovery is performed only if device configuration is empty. The data selection configuration is updated by discovery only if it is empty.

A successful discovery populates the device configuration and provides information such as segmentation and services that are supported. Optionally, the data selection configuration is also populated with the **Selected** parameter for all items set to `false`. For information about device configuration and data selection configuration, see [BACnet device configuration](xref:PIAdapterforBACnetDataSelectionConfiguration#device-configuration) and [Configure BACnet data selection](xref:PIAdapterforBACnetDataSelectionConfiguration#to-configure-data-selection).

The adapter [log](xref:LoggingConfiguration) indicates when discovery is complete.

### Example log

```log
[15:17:49 INF] [Bacnet] Discovering BACnet router.  
[15:18:19 INF] [Bacnet] Found 2 BACnet devices during discovery.
[15:18:19 INF] [Bacnet] Discovering BACnet device 1.  
[15:18:21 INF] [Bacnet] Discovery complete for BACnet device 1.  
[15:18:21 INF] [Bacnet] Discovering BACnet device 33.  
[15:18:53 INF] [Bacnet] Discovery complete for BACnet router.  
```
