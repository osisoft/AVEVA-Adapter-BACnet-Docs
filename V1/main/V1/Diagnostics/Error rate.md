---
uid: ErrorRate
---

# Error rate

The Diagnostics.Adapter.ErrorRate dynamic type includes these values, which are logged in a stream with the id {componentid}.ErrorRate.

| Type   | Property  | Description                                              |
| ------ | --------- | -------------------------------------------------------- |
| **string** | timestamp | Timestamp of event                                       |
| **double** | ErrorRate | 1-minute rolling average of error rate (streams/second)	|
