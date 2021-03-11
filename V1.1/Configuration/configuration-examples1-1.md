---
uid: PIAdapterForBACnetConfigurationExamples1-1
---

# PI Adapter for BACnet configuration examples

The following JSON samples provide examples for all configurations available for PI Adapter for BACnet.

## System components configuration with two BACnet adapter instances

```json
[
    {
        "ComponentId": "BACnet1",
        "ComponentType": "BACnet"
    },
    {
        "ComponentId": "BACnet2",
        "ComponentType": "BACnet"
    },
    {
        "ComponentId": "OmfEgress",
        "ComponentType": "OmfEgress"
    }
]
```

## Adapter configuration

```json
{
    "BACnet1": {
        "Logging": {
            "logLevel": "Information",
            "logFileSizeLimitBytes": 34636833,
            "logFileCountLimit": 31
        },
        "DataSource": {
            "IPAddress": "192.168.1.1",
            "Port": 47808,
            "MaxConcurrentNetworkRequests" : 0,
            "RequestDelay": "00:00:00",
            "AllowedConsecutiveFailedRequests": 3,
            "ReconnectInterval": "02:00:00"
        },
        "DataSelection": [
            {
                "DeviceId" : "Device1",
                "Selected": true,
                "Name": "MyDataItem",
                "UnitId": 1,
                "RegisterType": 3,
                "RegisterOffset": 123,
                "DataTypeCode": 20,
                "ScheduleId": "Schedule1",
                "StreamId": "stream.1",
                "BitMap": "020301",
                "ConversionFactor": 12.3,
                "ConversionOffset": 14.5,
                "DataFilterId" : "DataFilter1"
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
                "componentId": "BACnet1",
                "componentType": "BACnet"
            }
        ],
    "Buffering": {
            "BufferLocation": "C:/ProgramData/OSIsoft/Adapters/BACnet/Buffers",
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
            },
            {
                "Id": "EDS",
                "Endpoint": "http://localhost:/api/v1/tenants/default/namespaces/default/omf",
                "UserName": "eds",
                "Password": "eds"
            }
        ]
    }
}
```

## Data source configuration

The following are representations of data source configurations for the BACnet adapter.

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

## Data selection example

The following is an example of a valid BACnet data selection configuration with different data collection modes. Because the last item has **Selected** set to `false`, data will not be collected for it.

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
    "ScheduleId": "Schedule1"
  },
  {
    "Selected": true,
    "Name": "10.12.112.40_14.AnalogInput95",
    "StreamId": "10.12.112.40_14.AnalogInput95",
    "DeviceIPAddress": "10.12.112.40",
    "DeviceId": 14,
    "ObjectType": "AnalogInput",
    "ObjectId": 95,
    "DataCollectionMode": "SubscribeCovProperty",
    "PropertyIdentifier": "PresentValue",
    "CovIncrement": 0.5,
    "ScheduleId": "Schedule1"
  },
  {
    "Selected": false,
    "Name": "10.12.112.40_16.AnalogOutput70",
    "StreamId": "10.12.112.40_16.AnalogOutput70",
    "DeviceIPAddress": "10.12.112.40",
    "DeviceId": 16,
    "ObjectType": "AnalogOutput",
    "ObjectId": 70,
    "DataCollectionMode": "SubscribeCov",
    "ScheduleId": "Schedule2"
  }
]
```
