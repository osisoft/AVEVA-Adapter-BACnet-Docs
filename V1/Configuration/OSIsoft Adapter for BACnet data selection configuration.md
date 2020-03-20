---
uid: OSIsoftAdapterforBACnetDataSelectionConfiguration
---

# OSIsoft Adapter for BACnet data selection configuration

In addition to the data source configuration, you need to provide a data selection configuration to specify the data you want the BACnet adapter to collect from the data sources. 

When you add a data source, the BACnet adapter will discover devices and objects specified in the configuration.

## BACnet device configuration

During data source discovery, device information for all discovered devices is retrieved by the adapter, which is subsequently available through the following REST endpoint using any configuration tool that can execute an HTTP GET command: `http://localhost:5590/api/v1/configuration/<adapterId>/DeviceConfiguration/`.

**Note:** The device configuration is read only and only supports HTTP GET.

The device configuration may be used to choose an appropriate DataCollectionMode when configuring data selection. The following is an example of BACnet device configuration that contains one routed device:
```json
{
  419: {
    "DeviceIP": "10.12.8.64",
    "DeviceId": 419,
    "NetworkNumber": 20,
    "MacAddress": "ba:cb:00:5a:c4:16",
    "MaxApduSupported": 480,
    "SegmentationSupported": "MaxSegmentation",
    "ServicesSupported": [
      "WhoIs",    
      "IAm",
      "ReadProperty",
      "ReadPropertyMultiple"
    ]
  }
}
```

## Configure BACnet data selection

**Note:** You cannot modify BACnet data selection configurations manually. You must use the REST endpoints to add or edit the configuration.

Complete the following to configure the BACnet data selection:

1. Using any text editor, create a file that contains an BACnet data selection in JSON form.
    - For content structure, see [BACnet data selection example](#bacnet-data-selection-example).
    - For a table of all available parameters, see [BACnet data selection](#bacnet-data-selection-parameters).
2. Save the file, for example as _DataSelection.config.json_.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to execute a POST command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/<adapterId>/DataSelection/`

Example using curl (run this command from the same directory where the file is located):

**Note:** During installation, you can add a single BACnet adapter named BACnet1. The following example uses this component name.

```bash
curl -v -d "@DataSelection.config.json" -H "Content-Type: application/json" "http://localhost:5590/api/v1/configuration/BACnet1/DataSelection"
```

## BACnet data selection schema

The full schema definition for the BACnet data selection configuration is in the _BACnet_DataSelection_schema.json_ here:

Windows: *%Program Files%\OSIsoft\Adapters\BACnet\Schemas*

Linux: */opt/OSIsoft/Adapters/BACnet/Schemas*

## BACnet data selection parameters

The following parameters can be used to configure BACnet data selection:

| Parameter     | Required | Type | Nullable | Description |
|---------------|----------|------|----------|-------------|
| **Selected** | Optional | `boolean` | No | Use this field to select or clear a measurement. To select an item, set to true. To remove an item, leave the field empty or set to false.  If not configured, the default value is false.|
| **Name**      | Optional | `string` | Yes |The optional friendly name of the data item collected from the data source. If not configured, the default value will be the stream id. |
| **StreamID** | Optional | `string` | Yes | The custom stream ID used to create the streams. If not specified, the BACnet adapter will generate a default stream ID based on the measurement configuration. A properly configured custom stream ID follows these rules:<br><br>Is not case-sensitive.<br>Can contain spaces.<br>Cannot start with two underscores ("__").<br>Can contain a maximum of 100 characters.<br>Cannot use the following characters: / : ? # [ ] @ ! $ & ' ( ) \ * + , ; = % < > &#124;<br>Cannot start or end with a period.<br>Cannot contain consecutive periods.<br>Cannot consist of only periods. |
| **DeviceIPAddress** | Required | `string` | Yes | Device IP Address |
| **ObjectType** | Required | `string` | No | Any of the supported object types  |
| **ObjectId** | Required | `number` | Yes | BACnet object instance number |
| **DataCollectionMode** | Required | `string` | No | Specifies the mode of data collection for the item. Default and only value is Poll |
| **DataCollectionInterval** | Required | `number` | Yes | Specifies the interval (in seconds) at which data is collected for the item. Default value is 300 |
| **ObjectProperties** | Optional | `string[]` | Yes |  Specifies which properties to collect from the BACnet object. If left empty, PresentValue and StatusFlags are collected. Default is empty. |

## BACnet data selection example

The following is an example of valid BACnet data selection configuration. Since the second item has selected set to false, data will not be collected for it.

```json
[
 {
    "Selected": true,
    "Name": "10.12.112.40_14.AnalogInput90",
    "StreamId": "10.12.112.40_14.AnalogInput90",
    "DeviceIPAddress": "10.12.112.40",
    "DeviceId": 14,
    "ObjectType": "AnalogInput",
    "ObjectId": 90,
    "DataCollectionMode": "Poll",
    "DataCollectionInterval": 300,
  },
  {
    "Selected": false,
    "Name": "10.12.112.40_16.AnalogOutput70",
    "StreamId": "10.12.112.40_16.AnalogOutput70",
    "DeviceIPAddress": "10.12.112.40",
    "DeviceId": 16,
    "ObjectType": "AnalogOutput",
    "ObjectId": 70,
    "DataCollectionMode": "Poll",
    "DataCollectionInterval": 200,
    "ObjectProperties": ["PresentValue"]
  }
]
```
