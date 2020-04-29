---
uid: EgressEndpointsConfiguration
---

# Egress endpoints configuration

Adapters can egress dynamic data to destinations that you supply through OMF. Supported destinations are OSIsoft Cloud Services and PI servers through PI Web API.

An egress endpoint represents a destination to which data will be sent. You can specify multiple endpoints. Every egress endpoint is executed independently of all other egress endpoints and is expected to accept OMF messages. An egress endpoint is comprised of the properties specified under [Egress endpoint parameters](#egress-endpoint-parameters).

**Note:** Some types, and consequently containers and data, cannot be egressed.  For more information, see [Egress execution details](#egress-execution-details).

## Configure egress endpoints

**Note:** You cannot add egress configurations manually because some parameters are encrypted when stored to disk. You must use the REST endpoints to add or edit egress configuration. For additional endpoints, see [REST URLs](#rest-urls).

Complete the following procedure to create new egress endpoints:

1. Using any text editor, create a file that contains one or more egress endpoints in JSON form.
    - For content structure, see [Examples](#examples).
    - For a table of all available parameters, see [Egress endpoint parameters](#egress-endpoint-parameters).
3. Save the file, for example as _OmfEgress_DataEndpoints.config.json_.
4. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests and execute a POST command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints/`

    **Examples using curl:**

    - Add endpoints
        ```bash
        curl -d "@OmfEgress_DataEndpoints.config.json" -H "Content-Type: application/json" -X POST    "http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints"
        ```

        ```bash
        curl -d "@OmfEgress_DataEndpoints.config.json" -H "Content-Type: application/json" -X PUT   "http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints"
        ```

    - Delete an endpoint
        ```bash
        curl -X DELETE "http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints/{id}"
        ```

    - Update an endpoint
        ```bash
        curl -d "@OmfEgress_DataEndpoint.config.json" -H "Content-Type: application/json" -X UPDATE     "http://localhost:5590/api/v1/configuration/OmfEgress/dataendpoints/{id}"
        ```

    - View endpoints
        ```bash
        curl -X GET "http://localhost:5590/api/v1/configuration/OmfEgress/DataEndpoints"
        ```

## Egress endpoint configuration schema

The full schema definition for the egress endpoint configuration is in the *OmfEgress_DataEndpoints_schema.json* here:

Windows: *%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*


## Egress endpoint parameters

The following parameters are available for configuring egress endpoints:

| Parameter                       | Required                  | Type      | Nullable | Description                                        |
|---------------------------------|---------------------------|-----------|----------|-------------|
| **Id**                          | Required                  | `string`    | Yes      | Unique identifier |
| **Endpoint**                    | Required                  | `string`    | No      | Destination that accepts OMF v1.1 messages. Supported destinations include OCS and PI server. |
| **ValidateEndpointCertificate** | Optional                  | `boolean`   | No      | Disables verification of destination certificate. Use for testing only with self-signed certificates. Defaults to true. |
| **ClientId**                    | Required for OCS endpoint | `string`    | Yes      | Authentication with the OCS OMF endpoint. |
| **ClientSecret**                | Required for OCS endpoint | `string`    | Yes      | Authentication with the OCS OMF endpoint. |
| **TokenEndpoint**               | Optional for OCS endpoint | `string`    | Yes      | Retrieves an OCS token from an alternative endpoint. |
| **Username**                    | Required for PI endpoint  | `string`    | Yes      | Basic authentication to the PI Web API OMF endpoint. |
| **Password**                    | Required for PI endpoint  | `string`    | Yes      | Basic authentication to the PI Web API OMF endpoint. |


## Examples

The following examples are valid egress configurations.

**Egress data to OCS**

```json
[{
     "Endpoint": "https://<OCS OMF endpoint>",
     "ClientId": "<clientid>",
     "ClientSecret": "<clientsecret>"
}]
```

**Egress data to PI Web API.**

```json
[{
     "Endpoint": "https://<pi web api server>/piwebapi/omf/",
     "UserName": "<username>",
     "Password": "<password>"
    
}]
```

## REST URLs

| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/omfegress/DataEndpoints      | GET       | Gets all configured egress endpoints |
| api/v1/configuration/omfegress/DataEndpoints      | DELETE    | Deletes all configured egress endpoints |
| api/v1/configuration/omfegress/DataEndpoints      | POST      | Adds an array of egress endpoints or a single endpoint. Fails if any endpoint already exists |
| api/v1/configuration/omfegress/DataEndpoints      | PUT       | Replaces all egress endpoints |
| api/v1/configuration/omfegress/DataEndpoints/{id} | GET       | Gets configured endpoint by *id* |
| api/v1/configuration/omfegress/DataEndpoints/{id} | DELETE    | Deletes configured endpoint by *id* |
| api/v1/configuration/omfegress/DataEndpoints/{id} | PUT       | Replaces egress endpoint by *id*. Fails if endpoint doesn't exist |
| api/v1/configuration/omfegress/DataEndpoints/{id} | PATCH     | Allows partial updating of configured endpoint by *id* |

## Egress execution details

- After you add configuration for an egress endpoint, egress will be executed immediately for that endpoint. Egress is handled individually per configured endpoint. On first execution, types and containers will be egressed. After that only new or changed types or containers will be egressed. Type creation must be successful in order to create containers. Container creation must be successful in order to egress data.
- If an egress endpoint is removed, data flow will immediately stop for that endpoint. Buffered data of a removed endpoint will be permanently lost.
- Type, container, and data items are batched into one or more OMF messages when egressing. As per the requirements defined in OMF, a single message payload will not exceed 192KB in size. Compression is automatically applied to outbound egress messages. On the destination, failure to add a single item will result in the message failing. Types, containers, and data will continue to be egressed as long as the destination continues to respond to HTTP requests - retrying previous failures as needed.
