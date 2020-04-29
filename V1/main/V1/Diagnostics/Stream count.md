---
uid: StreamCount
---

# Stream count

The Diagnostics.StreamCountEvent dynamic type includes these values, which are logged in a stream with the id {componentid}.StreamCount. The stream count and type count include only types and streams created for sequential data received from a data source.

| Type   | Property    | Description                                       |
| ------ | ----------- | ------------------------------------------------- |
| **string** | timestamp   | Timestamp of event                                |
| **int**    | StreamCount | Number of streams created by the adapter instance |
| **int**    | TypeCount   | Number of types created by the adapter instance   |
