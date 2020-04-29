---
uid: BufferingConfiguration
---

# Buffering configuration

You can configure buffering for data egressed from the adapter to endpoints through the buffering configuration parameters in the system configuration.

**Note:** OSIsoft recommends that you do not modify the default buffering location unless necessary. The changes to the buffering configuration parameters take effect only during adapter service startup.

## Configure buffering

1. Using any text editor, create a file that contains the buffering configuration in JSON form.
   - For content structure, see the sample output in [Examples - Retrieve the buffering configuration](#examples).
   - For a table of all available parameters, see [Buffering parameters](#buffering-parameters).
2. Save the file.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests and execute a PUT command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/system/buffering`

     **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

     Example using curl (run this command from the same directory where the file is located): 

     ```
      curl -d "{ "MaxBufferSizeMB": 50, "BufferLocation": "C:/ProgramData/OSIsoft/Adapters/NewBuffers", "EnableBuffering": true }" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/system/buffering" 
      ```

## Buffering schema

The full schema definition for the system buffering is in the *System_Buffering_schema.json* here:

Windows: *%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*


## Buffering parameters

The following parameters are available for configuring buffering:

| Parameter | Required | Type | Description |
| ----------| -------- | ---- | ----------- |
| **EnableBuffering**  | Optional |  `boolean` | Enables or disables buffering. <br><br> Default: True |
| **MaxBufferSizeMB**  | Optional     |`Integer` | Defines the maximum size of the buffer file that will be persisted on disk. The unit is specified in MB (1 Mebibyte = 1048576 bytes). Take into account the capacity and type of the storage medium to determine a suitable value for this parameter. A value of -1 indicates that the buffer file size is restricted only by the available free disk space. <br><br> Allowed values: -1 or [1, 2147483647]. <br><br> Default: -1 |
| **BufferLocation**   | Required  | `string` | Defines the location of the buffer files. Absolute paths are required. Take into account access-control list (ACL) when setting this parameter <br><br> Allowed value: Valid path to a folder location in the file system. <br><br> Default: <br> **Windows:** _%ProgramData%\OSIsoft\Adapters\\{AdapterType}\\{AdapterInstance}\Data_ <br> **Linux:** _/usr/share/OSIsoft/Adapters/{AdatpterType}/{AdapterInstance}/Data_ |

## Examples

The following examples are buffering configurations made through curl REST client.

**Retrieve the buffering configuration**

```
curl -X GET "http://localhost:5590/api/v1/configuration/system/buffering"
```

Sample output:

```
{
    "bufferLocation": "C:/ProgramData/OSIsoft/Adapters/Modbus/Modbus/Buffers",
    "maxBufferSizeMB": -1,
    "enableBuffering": true
}
```

`200 OK` response indicates success.

**Update MaxBuferSizeMb parameter**

```
curl -d "{ "MaxBufferSizeMB": 100 }" -H "Content-Type: application/json" -X PATCH "http://localhost:5590/api/v1/configuration/system/buffering"
```

`204 No Content` response indicates success.

## REST URLs

| Relative URL | HTTP verb | Action               |
| ------------ |---------- |----------------------|
| api/v1/configuration/system/buffering | GET       | Gets the buffering configuration |
| api/v1/configuration/system/buffering | PUT       | Replaces the existing buffering configuration |
| api/v1/configuration/system/buffering | PATCH | Update parameter, partial configuration |
