---
uid: DeviceStatus
---

# Device Status

The device status indicates the health of this component and whether or not it is currently communicating properly with the data source. This time-series data is stored within a PI point or OCS stream, depending on the endpoint type. During healthy steady-state operation, a value of "Good" is expected.

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
