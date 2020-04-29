---
uid: BufferingConfiguration
---

# Overview

To configure buffering for the data egressed from the adapters to endpoints, you use buffering configuration parameters. These are global parameters and take effect only during startup. 

OSIsoft strongly recommends that you do not modify the default buffer configuration values.

> **Note:** This section describes the global parameters used for on-disk buffering configuration. For enabling or disabling buffering at the individual egress endpoint level using the *bufferingEnabled* field, see: <</INSERT LINK HERE>>

The parameters for on-disk buffering for the adapters that can be configured are:

| Parameter | Required | Type | Description |
| ----------|:--------:| ----:| :-----------|
| OnDiskMaxBufferSizeMB | Yes | Integer | Defines the maximum size of the buffer file that will be persisted on disk. The unit is specified in MB (Mebibyte 1 MiB = 1048576 bytes). You must take the capacity and type of the storage medium into account before you determine an alternative value for this parameter. For the case that you do not want to specify a maximum file size, a value of -1 indicates that the file size is restricted only by the available free disk space. <br> Allowed values: -1 or [1, 2147483647]. <br> Default: -1 | 
| OnDiskBufferLocation | Optional | String | Defines the location of the buffer file. Absolute paths are required. Take into account access-control list (ACL) when setting this parameter <br> Allowed value: Path to an existing folder location in the file system. <br> Default: **Windows:** _%ProgramData%\Adapters\Data_ <br> **Linux:** _/usr/share/OSIsoft/Adapters/Data_ |

## REST URLs

| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/egress/buffering      | GET       | Gets the buffering configuration |
| api/v1/configuration/egress/buffering      | PUT       | Replaces the existing buffering configuration |

## Examples
### Retrieve the buffering configuration through REST client
```
curl -X GET  http://localhost:{port}/api/v1/configuration/egress/buffering
```
Sample output:

```
{
    "onDiskBufferLocation": "C:\\ProgramData\\OSIsoft\\Adapters\\Data",
    "onDiskMaxBufferSizeMB": 10
}
```

### Configure buffer through REST client
```
curl -X PUT  http://localhost:{port}/api/v1/configuration/egress/buffering  -H 'Content-Type: application/json' -d '{ "onDiskMaxBufferSizeMB": 25,
"onDiskBufferLocation": "C:\\ProgramData\\OSIsoft\\Data"
}'
```
In the previous examples, *port* refers to the configured port for the adapter to run on.

If successful, the methods returns a `200 OK` response code.
