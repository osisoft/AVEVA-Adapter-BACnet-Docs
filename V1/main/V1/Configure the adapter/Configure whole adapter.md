---
uid: WholeAdapterConfiguration
---

# Configure whole adapter

You can configure OSIsoft System and adapter components entirely using a single call for replacing the existing configuration.

## Import configuration

### REST URLs

| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/     | PUT       | Replaces the configuration for the entire adapter  |

### Sample configuration file for OPC UA

The following sample includes configuration of System components along with an OPC UA adapter. 

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
	        "StreamIdPrefix": "OPC_Prefix_",
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
            "onDiskBufferLocation": "C:\\ProgramData\\OSIsoft\\Adapters\\Buffering",
            "onDiskMaxBufferSizeMB": -1
        }
    }
}
```

### Import full adapter configuration using REST client

- To import the full adapter configuration, run the following command:

```
curl -X http://localhost:5595/api/v1/configuration -d '{ JSON content }'
```

> **Note:** In order for some of the adapter specific configurations to take effect, you have to restart the adapter.

### Configuration errors

If the operation fails due to errors in the configuration, the count of the error and suitable error message(s) are returned in the result. 
