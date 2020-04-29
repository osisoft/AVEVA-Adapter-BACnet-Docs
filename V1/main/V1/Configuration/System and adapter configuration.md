---
uid: SystemAndAdapterConfiguration
---

# System and adapter configuration

You can configure the System and adapter components together using a single call for replacing the existing configuration.

## Change system and adapter configuration

Change the system and adapter configuration by importing the JSON file using a REST client:

1. Using any text editor, create a file that contains the System and adapter configuration in JSON form.
	- For content structure, see [Sample configuration file](#sample-configuration-file).
2. Save the file.
2. Use any of the [Configuration Tools](xref:ConfigurationTools) capable of making HTTP requests and execute a PUT command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration`

	Example using curl:
	
	```cmdline
	curl -d "@{JSON file name}" -H "Content-Type: application/json" -X  PUT "http://localhost:5590/api/v1/configuration"
	```

	**Note:** In order for some of the adapter specific configurations to take effect, you have to restart the adapter.

	If the operation fails due to errors in the configuration, the count of the error and suitable error message(s) are returned in the result.

## Sample configuration file

The following sample file shows the configuration of an OPC UA adapter. 

```json
{
    "OpcUa1": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "DataSource": {
            "EndpointUrl": "opc.tcp://OPCUAServerEndpoint/OPCUA/Server",
            "UseSecureConnection": false,
	    "StreamPrefix": "OPC_Prefix_",
            "UserName": null,
            "Password": null,
            "RootNodeIds": null,
            "IncomingTimestamp": "Source",
            "applyPrefixToStreamId": true
        },
        "DataSelection": [
            {
                "Selected": true,
                "Name": "Sawtooth",
                "NodeId": "ns=3;s=Sawtooth",
                "StreamId": "SawtoothStream"
            }
        ]
    },
    "System": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "HealthEndpoints": [
        ],
        "Components": [
            {
                "componentId": "Egress",
                "componentType": "OmfEgress"
            },
		    {
                "componentId": "OpcUa1",
                "componentType": "OpcUa"
            }
        ]
    },
    "Egress": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "DataEndpoints": [
            {
                "id": "WebAPI EndPoint",
                "endpoint": "https://PIWEBAPIServer/piwebapi/omf",
                "userName": "USERNAME",
                "password": "PASSWORD"
            },
            {
                "id": "OCS Endpoint",
                "endpoint": "https://OCSEndpoint/omf",
                "clientId": "CLIENTID",
                "clientSecret": "CLIENTSECRET"
            }
        ],
        "Buffering": {
            "BufferLocation": "C:\\ProgramData\\OSIsoft\\Adapters\\OpcUa\\OpcUa\\Buffers",
            "MaxBufferSizeMB": -1,
	    "EnableBuffering": true
        }
    }
}
```
 
## REST URLs

| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/     | PUT       | Replaces the configuration for the entire adapter  |
