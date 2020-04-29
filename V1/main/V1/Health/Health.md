---
uid: Health
---

# Adapter health

Adapters produce various types of health data. You can use this information to ensure that your adapters are running properly and data is flowing to the configured OSIsoft OMF endpoints. This section provides information on how to configure your adapters so that this health data is produced and stored at a designated endpoint and what types of health data are available.

## Configure health endpoints

A health endpoint designates an OSIsoft OMF endpoint where adapter health information should be sent. You can configure multiple health endpoints. 

1. Using any text editor, create a file that contains one or more health endpoints in JSON form.
    - For a table of all available health endpoint parameters, see [Parameters](#parameters).
2. Save the file.
3. Use any tool capable of making HTTP requests and execute a POST command with the contents of that file to the following endpoint: `

### Parameters

| Parameter                       | Required                            | Type      | Description                                        |
|---------------------------------|-------------------------------------|-----------|----------------------------------------------------|
| **Id**                          | Optional                            | `string`    | Uniquely identifies the endpoint. This can be any alphanumeric string. If left blank, a unique value is generated automatically. |
| **Endpoint**                    | Required                            | `string`    | The URL of the OMF endpoint to receive this health data. |
| **ClientId**                    | Required for OCS endpoints          | `string`    | The Client Id used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **ClientSecret**                | Required for OCS endpoints          | `string`    | The Client Secret used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **Username**                    | Required for PI Web API endpoints   | `string`    | The username used to authenticate with a PI Web API OMF endpoint. |
| **Password**                    | Required for PI Web API endpoints   | `string`    | The password used to authenticate with a PI Web API OMF endpoint. |
| **BufferingEnabled**            | Optional                            | `bool`      | Enables or disables buffering to this endpoint. By default, buffering is enabled ("true"). |
| **ValidateEndpointCertificate** | Optional                            | `bool`      | Disables verification of destination security certificate. Use for testing only with self-signed certificates; OSIsoft recommends setting this to true in production environments. Defaults to true. |

## Available health data
Each individual adapter data component produces a few different pieces of health data. Dynamic data is sent every minute to configured health endpoints.

The following health data are available:
- [Device status](xref:DeviceStatus)
- [Next Health Message Expected](xref:NextHealthMessageExpected)

## Health endpoint differences - PI Web API vs. OSIsoft Cloud Services

Two following two OMF endpoints are currently supported for adapter health data:

- PI Web API 
- OSIsoft Cloud Services

There are a few differences in how these two systems treat the associated health data. 

PI Web API parses the information and sends it configured PI Systems for the OMF endpoint. The static data is used to create a hierarchy on a PI AF server similar to the following:

![AdapterHealthAFHierarchy](AdapterHealthAFHierarchy.png)

The dynamic health data is actually time-series data that is stored in PI points on a PI Data Archive and can be seen in the AF hierarchy as PI Point Data Reference attributes.

OSIsoft Cloud Services currently does not have a way to store the static metadata. For OCS-based adapter health endpoints, only the dynamic data will be stored. Each value will be its own stream with the timestamp property as the single index.
