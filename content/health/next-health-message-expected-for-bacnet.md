---
uid: NextHealthMessageExpectedForBACnet
---

# Next health message expected

This property is similar to a heartbeat. A new value for `NextHealthMessageExpected` is sent by an individual adapter data component on a periodic basis while it is functioning properly. This value is a timestamp that indicates when the next value should be received. When monitoring, if the next value is not received by the indicated time, this likely means that there is an issue. It could be, for example, an issue with the adapter, an adapter component or the network connection between the health endpoint and the adapter.

| Property                          | Type                                 | Description                            |
|-----------------------------------|--------------------------------------|----------------------------------------|
| **Time**                          | `string`                             | Timestamp of the event                |
| **NextHealthMessageExpected**     | `string`                             | Timestamp when next value is expected |
