---
uid: PIAdapterBACnetDataSourceDiscovery
---

# BACnet data source discovery

When running a discovery against the data source of a BACnet adapter, you can specify optional query parameters. The query discovers the contents of the data source and narrows the scope of the discovery. Following a completed discovery, you can add the discovered items to the data selection.

## BACnet query syntax

When including a BACnet query within a discovery, you can query by DeviceId or MACAddress. Syntax for a BACnet query includes an identifier declaration followed by a comma-separated list of DeviceIds or MACAddresses for discovery. If you omit the identifier declaration, the query defaults to DeviceIds.

```text
<Identifier>=ID1,ID2,ID3 
```

## Query methods

When including a BACnet query within a discovery, you can query by DeviceId or MACAddress.

String item | Required | Description
--|--|--
DeviceIds | Optional | The device identifier for a BACnet device, which is a network-wide unique number. This identifier is a non-volatile value that is chosen and configured by someone at the site where the BACnet product is installed.
MACAddresses | Optional | The MACAddress for a BACnet device.

## Query examples

The query parameter of the BACnet component must be specified in one of the following forms:

* DeviceIds example: `DeviceIds=1,2,3,4,5`

    You can also query by DeviceId by omitting the `DeviceIds=` declaration: `1,2,3,4,5`

* MACAddress example: `MACAddresses=01-80-C2-00-00-10,01-80-C2-00-00-11,01-80-C2-00-00-12`

### BACnet data source discovery initiation

```json
<EXAMPLE_JSON_FOR_DISCOVERY_POST_REQUEST_THAT_INCLUDES_BACNET_QUERY>
```

### BACnet data source discovery results

```json
<EXAMPLE_JSON_FOR_DISCOVERY_GET_REQUEST>
```
