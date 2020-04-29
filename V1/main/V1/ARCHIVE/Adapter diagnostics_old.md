---
uid: AdapterDiagnosticsOld
---

# Adapter diagnostics

OSIsoft adapters produce diagnostic data which you can use to find more information about a particular adapter instance. This data lives alongside the health data and you can egress it using a Health Endpoint and setting EnableDiagnostics = true. 

For configuration of health endpoints, see </Health/Health.md>.

## AF hierarchy

When you use PI Web API as a health endpoint, an AF hierarchy is created containing both the diagnostics and health data and metadata. Currently, OSIsoft Cloud Services does not provide a way to store static metadata and only contains the dynamic streams. For more information or to see an example of this hierarchy, see </Health/Health.md>.

### Stream count

The stream count indicates the number of streams and associated types being produced and sent data for a particular adapter instance.

| Type         | Property |  Description     |
|--------|--------------|-----------------------------------|
| string | Timestamp | Timestamp of event |
| int | StreamCount | Overall number of streams created by the adapter instance |
| int | TypeCount | Overall number of types created by the adapter instance |

### IO rate

The IO rate indicates the running average number of streams per second being produced by an adapter instance.

| Type         | Property |  Description     |
|--------|--------------|-----------------------------------|
| string | Timestamp | Timestamp of event |
| double | IORate | Average data rate (streams/second) |

### Error rate

The error rate indicates the average number of errors per second occurring for a particular adapter instance.

| Type         | Property |  Description     |
|--------|--------------|-----------------------------------|
| string | Timestamp | Timestamp of event |
| double | ErrorRate | Average error rate (streams/second)
