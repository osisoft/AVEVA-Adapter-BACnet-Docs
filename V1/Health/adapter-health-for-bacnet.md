---
uid: AdapterHealthForBACnet
---

# Adapter health

PI Adapters produce different kinds of health data that can be egressed to different health endpoints.

## Available health data

Dynamic data is sent every minute to configured health endpoints.

The following health data are available:

- [Device status](xref:DeviceStatusForBACnet)
- [Next Health Message Expected](xref:NextHealthMessageExpectedForBACnet)

## AF structure

With a health endpoint configured to a PI server, you can use PI System Explorer to view the health of a given adapter. The element hierarchy is shown in the following image.

![Health data](../images/healthdata.PNG)