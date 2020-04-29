---
uid: AdapterDiagnostics
---

# Adapter diagnostics

The adapter and its components produce different kinds of diagnostics data which is sent to all health endpoints. The _System_Diagnostics.json_ file contains a flag which determines whether Diagnostics are enabled. You can change this at runtime through REST calls or the EdgeCmd utility. Diagnostics data are collected by default. 

To egress diagnostics related data, you have to configure an adapter health endpoint first. See [Health endpoint configuration](xref:HealthEndpointConfiguration).

## Available diagnostics data

Dynamic data is sent every minute to configured health endpoints.

The following diagnostics data are available:

- [System](xref:System)
- [Stream count](xref:StreamCount)
- [IO rate](xref:IORate)
- [Error rate](xref:ErrorRate)

## AF structure

After running diagnostics with a health endpoint configured to a PI server, you can use _**PI System Explorer**_ to view the diagnostics for a given adapter. The element hierarchy is shown in the following image. 

![System.Diagnostics](../images/Diagnostics_System.jpg)

- The_**Elements**_ root contains a link to an _**Adapters**_ node. This is the root note for all adapter instances.
- Below _**Adapters**_ there will be one or more adapter nodes. Each node's title is defined by the node's corresponding computer name and service name in this format: `_**{ComputerName}.{ServiceName}**_`. For example, in the following image, **_RGRALAK5530_** is the computer name, and _**SignalGenerator**_ is the service name.
- To see the **System.Diagnostics** values, clicking on an adapter node and set the tab to _**Attributes**_. Example values are shown in the image.
