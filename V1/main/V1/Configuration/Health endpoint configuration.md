---
uid: HealthEndpointConfiguration
---

# Health endpoint configuration

OSIsoft adapters can be configured to produce and store health data at a designated health endpoint.
For more information about adapter health, see [Adapter health](xref:AdapterHealth).

## Configure health endpoint

A health endpoint designates an OSIsoft OMF endpoint where adapter health information should be sent. You can configure multiple health endpoints. 

1. Using any text editor, create a file that contains one or more health endpoints in JSON form.
    - For a table of all available health endpoint parameters, see [Health endpoint parameters](#health-endpoint-parameters).
2. Save the file.
3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests and execute a POST command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/system/healthendpoints/`

## Health endpoints schema

The full schema definition for the health endpoint configuration is in the *System_HealthEndpoints_schema.json* here:

Windows: *%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*

## Health endpoint parameters

The following parameters are available for configuring health endpoints:

| Parameter                       | Required                            | Type      | Description                                        |
|---------------------------------|-------------------------------------|-----------|----------------------------------------------------|
| **Id**                          | Optional                            | `string`    | Uniquely identifies the endpoint. This can be any alphanumeric string. If left blank, a unique value is generated automatically. |
| **Endpoint**                    | Required                            | `string`    | The URL of the OMF endpoint to receive this health data. |
| **ClientId**                    | Required for OCS endpoints          | `string`    | The Client Id used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **ClientSecret**                | Required for OCS endpoints          | `string`    | The Client Secret used for authentication with an OSIsoft Cloud Services OMF endpoint. |
| **Username**                    | Required for PI Web API endpoints   | `string`    | The username used to authenticate with a PI Web API OMF endpoint. |
| **Password**                    | Required for PI Web API endpoints   | `string`    | The password used to authenticate with a PI Web API OMF endpoint. |
| **ValidateEndpointCertificate** | Optional                            | `boolean`      | Disables verification of destination security certificate. Use for testing only with self-signed certificates; OSIsoft recommends setting this to true in production environments. Defaults to true. |

# REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/Configuration/System/HealthEndpoints | GET | Retrieves all configured health endpoints |
| api/v1/Configuration/System/HealthEndpoints | POST | Adds a new PI Web API OMF or OCS health endpoint |
| api/v1/Configuration/System/HealthEndpoints/<endpointId> | PATCH | Updates or changes the values of a specific configured endpoint |
