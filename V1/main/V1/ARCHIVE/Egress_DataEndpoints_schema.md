---
uid: Egress_DataEndpoints_schema
---

# Egress endpoint configuration schema

```json
[{
        "endpoint": "https://<pi web api server>/piwebapi/omf/",
        "UserName": "<username>",
        "Password": "<password>"
    },
    {
        "Endpoint": "https://<OCS OMF endpoint>",
        "ClientId": "<clientid>",
        "ClientSecret": "<clientsecret>"
    }
]
```

| Abstract            | Extensible | Status       | Identifiable | Custom Properties | Additional Properties | Defined In                                                                             |
| ------------------- | ---------- | ------------ | ------------ | ----------------- | --------------------- | -------------------------------------------------------------------------------------- |
| Can be instantiated | Yes        | Experimental | No           | Forbidden         | Forbidden             | [Egress_DataEndpoints_schema.json](Egress_DataEndpoints_schema.json) |

# EgressEndpointConfiguration Properties

| Property                                                    | Type      | Required     | Nullable | Defined by                                |
| ----------------------------------------------------------- | --------- | ------------ | -------- | ----------------------------------------- |
| [ClientId](#clientid)                                       | `string`  | Optional     | Yes      | EgressEndpointConfiguration (this schema) |
| [ClientSecret](#clientsecret)                               | `string`  | Optional     | Yes      | EgressEndpointConfiguration (this schema) |
| [Endpoint](#endpoint)                                       | `string`  | **Required** | No       | EgressEndpointConfiguration (this schema) |
| [Id](#id)                                                   | `string`  | Optional     | Yes      | EgressEndpointConfiguration (this schema) |
| [Password](#password)                                       | `string`  | Optional     | Yes      | EgressEndpointConfiguration (this schema) |
| [TokenEndpoint](#tokenendpoint)                             | `string`  | Optional     | Yes      | EgressEndpointConfiguration (this schema) |
| [UserName](#username)                                       | `string`  | Optional     | Yes      | EgressEndpointConfiguration (this schema) |
| [ValidateEndpointCertificate](#validateendpointcertificate) | `boolean` | Optional     | No       | EgressEndpointConfiguration (this schema) |

## ClientId

`ClientId`

- is optional
- type: `string`
- defined in this schema

### ClientId Type

`string`, nullable

## ClientSecret

`ClientSecret`

- is optional
- type: `string`
- defined in this schema

### ClientSecret Type

`string`, nullable

## Endpoint

`Endpoint`

- is **required**
- type: `string`
- defined in this schema

### Endpoint Type

`string`

- minimum length: 1 characters

## Id

`Id`

- is optional
- type: `string`
- defined in this schema

### Id Type

`string`, nullable

## Password

`Password`

- is optional
- type: `string`
- defined in this schema

### Password Type

`string`, nullable

## TokenEndpoint

`TokenEndpoint`

- is optional
- type: `string`
- defined in this schema

### TokenEndpoint Type

`string`, nullable

## UserName

`UserName`

- is optional
- type: `string`
- defined in this schema

### UserName Type

`string`, nullable

## ValidateEndpointCertificate

`ValidateEndpointCertificate`

- is optional
- type: `boolean`
- defined in this schema

### ValidateEndpointCertificate Type

`boolean`

**All** of the following _requirements_ need to be fulfilled.

#### Requirement 1

`object` with following properties:

| Property                      | Type    | Required     |
| ----------------------------- | ------- | ------------ |
| `ClientId`                    | string  | Optional     |
| `ClientSecret`                | string  | Optional     |
| `Endpoint`                    | string  | **Required** |
| `Id`                          | string  | Optional     |
| `Password`                    | string  | Optional     |
| `TokenEndpoint`               | string  | Optional     |
| `UserName`                    | string  | Optional     |
| `ValidateEndpointCertificate` | boolean | Optional     |

#### ClientId

`ClientId`

- is optional
- type: `string`

##### ClientId Type

`string`, nullable

#### ClientSecret

`ClientSecret`

- is optional
- type: `string`

##### ClientSecret Type

`string`, nullable

#### Endpoint

`Endpoint`

- is **required**
- type: `string`

##### Endpoint Type

`string`

- minimum length: 1 characters

#### Id

`Id`

- is optional
- type: `string`

##### Id Type

`string`, nullable

#### Password

`Password`

- is optional
- type: `string`

##### Password Type

`string`, nullable

#### TokenEndpoint

`TokenEndpoint`

- is optional
- type: `string`

##### TokenEndpoint Type

`string`, nullable

#### UserName

`UserName`

- is optional
- type: `string`

##### UserName Type

`string`, nullable

#### ValidateEndpointCertificate

`ValidateEndpointCertificate`

- is optional
- type: `boolean`

##### ValidateEndpointCertificate Type

`boolean`
