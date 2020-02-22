---
uid: OSIsoftAdapterforBACnetDataSelectionConfiguration
---

# OSIsoft Adapter for BACnet data selection configuration

In addition to the data source configuration, you need to provide a data selection configuration to specify the data you want the BACnet adapter to collect from the data sources. 

When you add a data source, the BACnet adapter browses the entire BACnet server address space and exports the available BACnet variables into a JSON file for data selection. Data is collected automatically based upon user demands. BACnet data from BACnet variables is read through subscriptions (unsolicited reads).

You can either have the data selection configuration file generated for you or you can create it manually yourself.

## Generate default BACnet data selection configuration file

A default BACnet data selection file will be created if there is no BACnet data selection configuration, but a valid BACnet data source exists.

**Note:** To avoid possibly expensive browse operations, OSIsoft recommends that you manually create a data selection file instead of generating the default data selection file. For more information, see [Configure BACnet data selection](#configure-bacnet-data-selection).

Complete the following procedure for this default data selection file to be generated:

1. Add an BACnet adapter with a unique ComponentId. For more information, see [System components configuration](xref:SystemComponentsConfiguration).

  During the installation of Edge Data Store, enabling the BACnet adapter results in addition of a unique component that also satisfies this condition.
  
2. Configure a valid BACnet data source. For more information, see [OSIsoft Adapter for BACnet data source configuration](xref:OSIsoftAdapterforBACnetDataSourceConfiguration).

  Once you complete these steps, a default BACnet data selection configuration file will be generated in the configuration directory for the corresponding platform.
  
  The following are example locations of the file created. In this example, it is assumed that the ComponentId of the BACnet component is the default BACnet1:

  Windows: *%programdata%\OSIsoft\Adapters\BACnet\Configuration\BACnet1_DataSelection.json*
   
  Linux: */usr/share/OSIsoft/Adapters/BACnet/Configuration/BACnet1_DataSelection.json*

3. Copy the file to a different directory.

  The contents of the file will look something like:

  ```json
[
    {
      "Selected": true,
      "Name": "Bacnet1",
      "StreamId": "CustomStreamName",
      "DeviceIPAddress": "10.12.112.38",
      "DeviceId": 14,
      "ObjectType": "AnalogInput",
      "ObjectId": 90,
      "DataCollectionMode": "Poll",
      "DataCollectionInterval": 300
    }
]
  ```

4. In a text editor, edit the file and change the value of any Selected key from false to true in order to transfer the BACnet data to be stored in Edge Data Store. 
5. In the same directory where you edited the file, run the following curl command:

  ```bash
  curl -i -d "@BACnet1_DataSelection.json" -H "Content-Type: application/json" -X PUT http://localhost:5590/api/v1/configuration/BACnet1/Dataselection
  ```

## BACnet device configuration

During data source discovery, device information for all discovered devices is retrieved by the adapter, which is subsequently available through the following REST endpoint using any configuration tool that can execute an HTTP GET command: `http://localhost:5590/api/v1/configuration/<adapterId>/DeviceConfiguration/`.

**Note:** The device configuration is read only and only supports HTTP GET.

The device configuration may be used to choose an appropriate DataCollectionMode when configuring data selection. The following is an example of BACnet device configuration that contains one routed device:
```json
{
  "10.12.8.64_419": {
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

The following table shows the basic behavior of the _BACnet_DataSelection_schema.json_ file.

| Abstract            | Extensible | Status       | Identifiable | Custom properties | Additional properties |
| ------------------- | ---------- | ------------ | ------------ | ----------------- | --------------------- |
| Can be instantiated | Yes        | Experimental | No           | Forbidden         | Forbidden             |

The full schema definition for the BACnet data selection configuration is in the _BACnet_DataSelection_schema.json_ here:

Windows: *%Program Files%\OSIsoft\Adapters\BACnet\Schemas*

Linux: */opt/OSIsoft/Adapters/BACnet/Schemas*

## BACnet data selection parameters

The following parameters can be used to configure BACnet data selection:

| Parameter     | Required | Type | Nullable | Description |
|---------------|----------|------|----------|-------------|
| **Selected** | Optional | `boolean` | No | Use this field to select or clear a measurement. To select an item, set to true. To remove an item, leave the field empty or set to false.  If not configured, the default value is false.|
| **Name**      | Optional | `string` | Yes |Friendly name for the item. By default, this will be a combination of DeviceIPAddress, DeviceId, ObjectType, and ObjectId in the format [DeviceIPAddress]_[DeviceId].[ObjectType][ObjectId] |
| **StreamID** | Optional | `string` | Yes | Custom stream ID for the item. This allows users to use custom “tag names” for items that are being collected. By default, this will be a combination of DeviceIPAddress, DeviceId, ObjectType, and ObjectId in the format [DeviceIPAddress]_[DeviceId].[ObjectType][ObjectId] |
| **DeviceIPAddress** | Required | `string` | Yes | Device IP Address |
| **ObjectType** | Required | `enum` | No | Specifies the mode of data collection for the item. Options: Poll |
| **ObjectId** | Required | `int` | Yes | BACnet object instance number |
| **DataCollectionMode** | Required | `enum` | No | Specifies the mode of data collection for the item. Default value is Poll |
| **DataCollectionInterval** | Required | `int` | Yes | Specifies the interval (in seconds) at which data is collected for the item. Default value is 300 |
| **ObjectProperties** | Optional | `string[]` | Yes |  Specifies which properties to collect from the BACnet object. If left empty, Present_Value and Status_Flags are collected. Default is empty. |

## BACnet data selection example

The following is an example of valid BACnet data selection configuration:

```json
[
 {
    "Selected": true,
    "Name": "Bacnet1",
    "StreamId": "CustomStreamName",
    "DeviceIPAddress": "10.12.112.38",
    "DeviceId": 14,
    "ObjectType": "AnalogInput",
    "ObjectId": 90,
    "DataCollectionMode": "Poll",
    "DataCollectionInterval": 300,
  },
  {
    "Selected": false,
    "Name": "Bacnet2",
    "StreamId": "CustomStreamName2",
    "DeviceIPAddress": "10.12.112.40",
    "DeviceId": 16,
    "ObjectType": "AnalogOutput",
    "ObjectId": 70,
    "DataCollectionMode": "Poll",
    "DataCollectionInterval": 200,
    "ObjectProperties": ["AckRequired", "Present_Values"]
  }
]
```
