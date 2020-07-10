---
uid: DeviceStatusForBACnet
---

# Device status

The device status indicates the health of the component and if it is currently communicating properly with the data source. This time-series data is stored within a PI point or OCS stream, depending on the endpoint type. The BACnet adapter sends a status value of `Good` when all configured BACnet devices and routers respond within the specified timeout. When a BACnet device fails to respond to more than one **AllowedConsecutiveFailedRequests** (see [PI Adapter for BACnet data source configuration](xref:PIAdapterforBACnetDataSourceConfiguration), it is considered disconnected and a `DeviceInError` status is sent. For any individual device that transitions from connected to disconnected and vice versa, an appropriate status is sent depending on if there are one or more disconnected devices, `DeviceInError` or all are connected, `Good`.

| Property                          | Type                                 | description                    |
|-----------------------------------|--------------------------------------|--------------------------------|
| **Time**                          | `string`                               | Timestamp of the event        |
| **DeviceStatus**                  | `string`                               | The value of the `DeviceStatus` |

The possible statuses:

| Status                            | Meaning                               |
|-----------------------------------|---------------------------------------|
| `Good`                          | The component is connected to the data source and it is collecting data. |
| `ConnectedNoData`               | The component is connected to the data source but it is not receiving data from it. |
| `AttemptingFailover`            | The adapter is attempting to failover. |
| `Starting`                      | The component is currently in the process of starting up and is not yet connected to the data source. |
| `DeviceInError`                 | The component encountered an error either while connecting to the data source or attempting to collect data. |
| `Shutdown`                      | The component is either in the process of shutting down or has finished. |
| `Removed`                       | The adapter component has been removed and will no longer collect data. |
| `NotConfigured`                 | The adapter component has been created but is not yet configured. |
