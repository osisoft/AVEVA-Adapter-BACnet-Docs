---
uid: DeviceStatusForBACnet
---

# Device status

The device status indicates the health of this component and if it is currently communicating properly with the data source. This time-series data is stored within a PI point or OCS stream, depending on the endpoint type. The BACnet Adapter will send a status value of "Good" when all configured BACnet devices and routers are responding within the specified timeout. When a BACnet device fails to respond to more than AllowedConsecutiveFailedRequests (see [OSIsoft Adapter for BACnet data source configuration](xref:OSIsoftAdapterforBACnetDataSourceConfiguration)), it is considered disconnected and a "DeviceInError" status is sent. Upon any individual device transitioning from connected to disconnected or back, an appropriate status is sent depending on if there are one or more disconnected devices (DeviceInError) or all are connected (Good).

| Property                          | Type                                 | Description                    |
|-----------------------------------|--------------------------------------|--------------------------------|
| **Time**                          | `string`                               | Timestamp of the event.        |
| **DeviceStatus**                  | `string`                               | The value of the DeviceStatus. |

The possible statuses are:

| Status                            | Meaning                               |
|-----------------------------------|---------------------------------------|
| **Good**                          | The component is connected to the data source and it is collecting data. |
| **ConnectedNoData**               | The component is connected to the data source but it is not receiving data from it. |
| **AttemptingFailover**            | The adapter is attempting to failover. |
| **Starting**                      | The component is currently in the process of starting up and is not yet connected to the data source. |
| **DeviceInError**                 | The component encountered an error either while connecting to the data source or attempting to collect data. |
| **Shutdown**                      | The component is either in the process of shutting down or has finished. |
| **Removed**                       | The adapter component has been removed and will no longer collect data. |
| **NotConfigured**                 | The adapter component has been created but is not yet configured. |
