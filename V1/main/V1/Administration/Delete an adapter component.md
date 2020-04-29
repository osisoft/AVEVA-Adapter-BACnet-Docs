---
uid: DeleteAnAdapterComponent
---

# Delete an adapter component

When an adapter component is removed, the configuration and log files are saved into a sub-directory in case they are needed later. Any associated types, streams, and data will remain on respective endpoints.

Complete the following procedure to delete an adapter component:

1. Start any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests.

2. Execute a DELETE command to the following endpoint: `http://localhost:5590/api/v1/configuration/system/components/<ComponentId>`

    **Note:** An empty DELETE command must be made against the Id of the component to be deleted. 

      Example using curl - Delete OpcUa1 adapter component

      ```bash
      curl -v -X DELETE "http://localhost:5590/api/v1/configuration/system/components/OpcUa1"
      ```

## File relocation

All configuration and log files will be renamed and moved.The files are renamed according to the timestamp of removal, for example *FileName.json_removed_yyyy-MM-dd--hh-mm-ss*. 

Configuration files will be moved to the following location:

   **Windows:** *%programdata%\OSIsoft\Adapters\AdapterName\AdapterName\Configuration\Removed*

   **Linux:** */usr/share/OSIsoft/Adapters/AdapterName/AdapterName/Configuration/Removed*

Log files will be moved to the following location:

   **Windows:** *%programdata%\OSIsoft\Adapters\AdapterName\AdapterName\Logs\Removed*

   **Linux:** */usr/share/OSIsoft/Adapters/AdapterName/AdapterName/Logs/Removed*

In the following example, one Modbus Adapter service is installed on a particular Windows node with the name ModbusService1. A Modbus component with the name ModbusDeviceX was added and configured to this Modbus adapter and later removed. Linux follows a similar behavior. This is the resulting relocation and renaming scheme after deletion:

![ConfigurationFolder](../images/ConfigurationFolder.png)

![RemovedConfigurations](../images/RemovedConfigurations.png)

![LogsFolder](../images/LogsFolder.png)

![RemovedLogs](../images/RemovedLogs.png)


## REST URLs
| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/system/components/{id}      | DELETE       | Deletes specified component |

**Note:** {id} is the ID of the component that you want to remove, for example OpcUa1 or Modbus1.
