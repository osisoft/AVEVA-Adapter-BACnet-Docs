---
uid: PIAdapterBACnetDataSourceDiscovery
---

# BACnet data source discovery

When running a discovery against the data source of a BACnet adapter, you can specify optional query parameters. The query discovers the contents of the data source and narrows the scope of the discovery. Following a completed discovery, you can add the discovered items to the data selection.

## BACnet query syntax

When including a BACnet query within a discovery, you can query by using one of two methods: DeviceId or MACAddress. For more information, see [Query methods](#query-methods).

Syntax for a BACnet query includes a query method declaration followed by a comma-separated list of DeviceIds or MACAddresses for discovery. If you omit the query method declaration, the method defaults to `DeviceIds`.

```text
<QUERY_METHOD>=<ID1>,<ID2>,<ID3> 
```

Within the API request JSON payload, enter the BACnet query using the `query` parameter, as shown in the example below. For more information on using the query parameter during API requests to the `api/v1/configuration/<componentId>/discoveries` endpoint, see <xref:DiscoveryConfiguration>.

```json
{
    "id" : "40",
    "query" : "DeviceIds=1,2,3,4,5"
}
```

## Query methods

When including a BACnet query within a discovery, you can query by one of two methods: DeviceId or MACAddress.

String item | Required | Description
--|--|--
DeviceIds | Optional | The device identifier for a BACnet device, which is a network-wide unique number. This identifier is a non-volatile value that is chosen and configured by someone at the site where the BACnet product is installed.
MACAddresses | Optional | The MACAddress for a BACnet device.

## Query examples

The query parameter of the BACnet component must be specified in one of the following forms:

### DeviceIds example

When querying by `DeviceIds`, follow the `DeviceIds` declaration with a list of the device identifiers you are searching for:

```text
DeviceIds=1,2,3,4,5
```

You can also query by DeviceId by omitting the `DeviceIds=` declaration:

```text
1,2,3,4,5
```

Within the API request JSON payload, a BACnet by DeviceId will look something like this:

```json
{
    "id" : "40",
    "query" : "DeviceIds=1,2,3,4,5"
}
```

### MACAddress example

When querying by `MACAddresses`, follow the `MACAddresses` declaration with a list of MACAddresses you are searching for.

```text
MACAddresses=01-80-C2-00-00-10,01-80-C2-00-00-11,01-80-C2-00-00-12
```

Within the API request JSON payload, a BACnet query by MACAddress will look something like this:

```json
{
    "id" : "45",
    "query" : "MACAddresses=01-80-C2-00-00-10,01-80-C2-00-00-11,01-80-C2-00-00-12"
}
```
