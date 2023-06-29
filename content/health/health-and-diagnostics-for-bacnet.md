---
uid: HealthAndDiagnosticsForBACnet
---

# Health and diagnostics

AVEVA Adapters produce various types of health data. You can use health data to ensure that your adapters are running properly and that data flows to the configured OMF endpoints. For more information, see [Adapter health](xref:AdapterHealthForBACnet).

AVEVA Adapters also produce diagnostic data. You can use diagnostic data to find more information about a particular adapter instance. Diagnostic data lives alongside the health data and you can egress it using a health endpoint and setting `EnableDiagnostics`to `true`. You can configure `EnableDiagnostics` in the system's [General configuration](xref:GeneralConfiguration). For more information on available diagnostics, see [Adapter diagnostics](xref:AdapterDiagnostics).

## Health endpoint differences

Two OMF endpoints are currently supported for adapter health data:

- PI Web API
- AVEVA Data Hub

There are a few differences in how these two systems treat the associated health and diagnostics data.

- PI Web API parses the information and sends it to configured PI servers for the OMF endpoint. The static data is used to create a hierarchy on a PI AF server similar to the following example:

  ![AdapterHealthAFHierarchy](../images/adapter-health-af-hierarchy.png)

  The dynamic health data is time-series data that is stored in PI points on a PI Data Archive. You can see it in the AF hierarchy as PI point data reference attributes.

- AVEVA Data Hub does not currently provide a way to store the static metadata. For ADH-based adapter health endpoints, only the dynamic data is stored. Each value is its own stream with the timestamp property as the single index.
