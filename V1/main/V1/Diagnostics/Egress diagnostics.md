---
uid: EgressDiagnostics
---

# Egress diagnostics

The Egress component of the adapter produces the following diagnostics streams.

## IO rate

The Diagnostics.Egress.IORate dynamic type includes these values, which are logged in a stream with the id {machineName}.{serviceName}.OmfEgress.{EndpointId}.IORate. IO rate includes only sequential data sucessfully sent to an egress.

| Type   | Property  | Description                                            	|
| ------ | --------- | -------------------------------------------------------	|
| **string** | timestamp | Timestamp of event                                    	|
| **double** | IORate    | 1-minute rolling average of data rate (streams/second)	|
