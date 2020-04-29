---
uid: DeleteAdapter
---

# Delete an Adapter

An adapter instance can be removed by making a DELETE call with either a REST client or the EdgeCmd utility. When an adapter instance is removed, the configuration and log files are saved into a sub-directory in case they are needed later. Any associated types, streams, and data will remain on respective endpoints.

## File Relocation

All configuration and log files will be renamed and moved to a folder called "Removed" within the respective directory. Configuration files will be moved to .\Configuration\Removed; logs files to .\Logs\Removed. The files are renamed according to the timestamp of removal, e.g. FileName.json_removed_yyyy-MM-dd--hh-mm-ss.

In the following example, one Modbus Adapter service is installed on a particular Windows node with the name "ModbusService1". A Modbus component with the name "ModbusDeviceX" was added and configured to this Modbus adapter and later removed. Similar behavior will be seen on Linux. This is the resulting relocation and renaming scheme after deletion:

![ConfigurationFolder](ConfigurationFolder.png)

![RemovedConfigurations](RemovedConfigurations.png)

![LogsFolder](LogsFolder.png)

![RemovedLogs](RemovedLogs.png)


## REST Command: DELETE

An empty DELETE command must be made against the Id of the component to be deleted. Using cURL:

```bash
curl -v -X DELETE "http://localhost:5595/api/v1/configuration/system/components/ComponentIdToBeDeleted"
```

## REST URLs
| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/system/components/{id}      | DELETE       | Deletes specified component |