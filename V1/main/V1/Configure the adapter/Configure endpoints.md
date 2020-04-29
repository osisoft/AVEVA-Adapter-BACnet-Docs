---
uid: ConfigureEndpoints
---

# Configure endpoints

Adapters can egress dynamic data to destinations that you supply through OMF. Supported destinations are OSIsoft Cloud Services and PI servers through PI Web API.

An egress endpoint represents a destination to which data will be sent. You can specify multiple endpoints. Every egress endpoint is executed independently of all other egress endpoints and is expected to accept OMF messages. An egress endpoint is comprised of the properties specified under [Parameters](#parameters).

> **Note:** Some types, and consequently containers and data, cannot be egressed.  For more information, see [Egress Execution Details](#egress-execution-details).

## Configuration procedure

> **Note:** You cannot add egress configurations manually because some parameters are encrypted when stored to disk. You must use the REST endpoints to add or edit egress configuration. For additional endpoints, see [REST URLs](#rest-urls).

Complete the following to create new egress endpoints:

1. Using any text editor, create a file that contains one or more egress endpoints in JSON form.
    - For content structure, see [Examples](#examples).
    - For a table of all available egress parameters, see [Parameters](#parameters).
2. Save the file.
3. Use any tool capable of making HTTP requests and execute a POST command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/Egress/dataendpoints/`

**Example using cURL:**

- Add endpoints
    ```bash
    curl -v -d "@Egress_DataEndpoints.config.json" -H "Content-Type: application/json" -X POST      "http://localhost:5590/api/v1/configuration/Egress/dataendpoints"
    ```

    ```bash
    curl -v -d "@Egress_DataEndpoints.config.json" -H "Content-Type: application/json" -X PUT   "http://localhost:5590/api/v1/configuration/Egress/dataendpoints"
    ```

- Delete an endpoint
    ```bash
    curl -v -X DELETE "http://localhost:5590/api/v1/configuration/Egress/dataendpoints/{id}"
    ```

- Update an endpoint
    ```bash
    curl -v -d "@Egress_DataEndpoint.config.json" -H "Content-Type: application/json" -X UPDATE     "http://localhost:5590/api/v1/configuration/Egress/dataendpoints/{id}"
    ```

- View endpoints
    ```bash
    curl -v -X GET "http://localhost:5590/api/v1/configuration/Egress/DataEndpoints"
    ```

### Parameters

| Parameter                       | Required                  | Type      | Description                                        |
|---------------------------------|---------------------------|-----------|----------------------------------------------------|
| **Id**                          | Required                  | string    | Unique identifier |
| **Endpoint**                    | Required                  | string    | Destination that accepts OMF v1.1 messages. Supported destinations include OCS and PI server. |
| **ClientId**                    | Required for OCS endpoint | string    | Authentication with the OCS OMF endpoint. |
| **ClientSecret**                | Required for OCS endpoint | string    | Authentication with the OCS OMF endpoint. |
| **TokenEndpoint**               | Optional for OCS endpoint | string    | Retrieves an OCS token from an alternative endpoint. |
| **Username**                    | Required for PI endpoint  | string    | Basic authentication to the PI Web API OMF endpoint. |
| **Password**                    | Required for PI endpoint  | string    | Basic authentication to the PI Web API OMF endpoint. |
| **ValidateEndpointCertificate** | Optional                  | boolean   | Disables verification of destination certificate. Use for testing only with self-signed certificates. Defaults to true. |

### Examples

The following examples are valid egress configurations.

**Egress data to OCS**

```json
[{
    "Id": "OCS",
    "Endpoint" : " https://{IP/FQDN of OCS}/api/Tenants/{tenantId}/Namespaces/{namespaceId}/omf",
    "ClientId" : "{clientId}",
    "ClientSecret" : "{clientSecret}"
}]
```

**Egress data to PI Web API.**

```json
[{
    "Id": "PI WebAPI",
    "Endpoint" : " https://{IP/FQDN of WebApi}/piwebapi/omf",
    "userName" : "{username}",
    "Password" : "{password}"
}]
```

### REST URLs

| Relative URL                                              | HTTP verb | Action               |
|-----------------------------------------------------------|-----------|----------------------|
| api/v1/configuration/egress/DataEndpoints      | GET       | Gets all configured egress endpoints |
| api/v1/configuration/egress/DataEndpoints      | DELETE    | Deletes all configured egress endpoints |
| api/v1/configuration/egress/DataEndpoints      | POST      | Adds an array of egress endpoints or a single endpoint. Fails if any endpoint already exists |
| api/v1/configuration/egress/DataEndpoints      | PUT       | Replaces all egress endpoints |
| api/v1/configuration/egress/DataEndpoints/{id} | GET       | Gets configured endpoint by *id* |
| api/v1/configuration/egress/DataEndpoints/{id} | DELETE    | Deletes configured endpoint by *id* |
| api/v1/configuration/egress/DataEndpoints/{id} | PUT       | Replaces egress endpoint by *id*. Fails if endpoint doesn't exist |
| api/v1/configuration/egress/DataEndpoints/{id} | PATCH     | Allows partial updating of configured endpoint by *id* |

## Egress execution details

- After you add configuration for an egress endpoint, egress will be executed immediately for that endpoint. Egress is handled individually per configured endpoint. On first execution, types and containers will be egressed. After that only new or changed types or containers will be egressed. Type creation must be successful in order to create containers. Container creation must be successful in order to egress data.
- If an egress endpoint is removed, data flow will immediately end for that endpoint. Any buffered data for the endpoint that has been deleted will be permanently lost.
- Type, container, and data items are batched into one or more OMF messages when egressing. As per the requirements defined in OMF, a single message payload will not exceed 192KB in size. Compression is automatically applied to outbound egress messages. On the destination, failure to add a single item will result in the message failing. Types, containers, and data will continue to be egressed as long as the destination continues to respond to HTTP requests - retrying previous failures as needed.
