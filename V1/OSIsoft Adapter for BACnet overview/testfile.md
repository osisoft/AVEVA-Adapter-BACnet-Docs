 <details><summary>
Click to see the code.
  </summary>
 
```python
print("hello world!")
``` 

  </details>


---
uid: SystemAndAdapterConfiguration
---

# System and adapter configuration

The System and adapter components can be configured together using a single call for replacing the existing configuration.

## Change system and adapter configuration

Change the system and adapter configuration by importing the JSON file using a REST client:

1. Using any text editor, create a file that contains the System and adapter configuration in JSON form.
    - For content structure, see [Example](#example).
2. Save the file, for example as *SystemAdapter.config.json*.
3. Use any of the [Configuration Tools](xref:ConfigurationTools) capable of making HTTP requests and execute a PUT command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration`

    **Note:** `5590` is the default port number. If you selected a different port number, replace it with that value.

    Example using curl (run this file from the same directory where the file is located):

    ```bash
    curl -d "@SystemAdapter.config.json" -H "Content-Type: application/json" -X  PUT "http://localhost:5590/api/v1/configuration"
    ```

    **Note:** In order for some of the adapter specific configurations to take effect, you have to restart the adapter.

    If the operation fails due to errors in the configuration, the count of the error and suitable error message(s) are returned in the result.

## Examples

### Sample configuration file

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
    "Diagnostics": {
            "enableDiagnostics": true
    },
        "Components": [
            {
                "componentId": "Egress",
                "componentType": "OmfEgress"
            },
            {
                "componentId": "OpcUa1",
                "componentType": "OpcUa"
            }
        ],
    "Buffering": {
            "BufferLocation": "C:/ProgramData/OSIsoft/Adapters/OpcUa/OpcUa/Buffers",
            "MaxBufferSizeMB": -1,
            "EnableBuffering": true
        }
     },
    "OmfEgress": {
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
        ]

    }
}
```
