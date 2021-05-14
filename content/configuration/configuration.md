---
uid: BACnetConfiguration
---

# Configuration

PI Adapter for BACnet provides configuration of data source and data selection. The adapter also provides the ability to generate a data selection file instead of manual configuration.

The examples in the configuration topics use `curl`, a commonly available tool on both Windows and Linux. The adapter can be configured with any programming language or tool that supports making REST calls, or with the EdgeCmd utility. For more information, see the [EdgeCmd utility documentation (https://osisoft.github.io/Edgecmd-Docs/content/edgecmd-utility.html)](https://osisoft.github.io/Edgecmd-Docs/content/edgecmd-utility.html). To validate successful configurations, you can perform data retrieval (GET commands) using a browser, if available on your device.

For more information on PI Adapter configuration tools, see [Configuration tools](xref:ConfigurationTools).

## Quick start

Complete the following steps to establish a data flow from a BACnet data source device to a data endpoint.

1. Configure one or several BACnet system components.

    See <xref:SystemComponentsConfiguration>.

1. Configure a BACnet data source for each BACnet device.

    See <xref:PIAdapterforBACnetDataSourceConfiguration>.

1. Configure a BACnet data selection for each BACnet data source.

    See <xref:PIAdapterforBACnetDataSelectionConfiguration>.

1. Configure one or several egress endpoints.

    See <xref:EgressEndpointsConfiguration>.
