---
uid: BACnetConfiguration
---

# Configuration

PI Adapter for BACnet provides configuration of data source and data selection. The adapter also provides the ability to generate a data selection file instead of manual configuration.

<<<<<<< HEAD
The examples in the configuration topics use `curl`, a commonly available tool on both Windows and Linux. The adapter can be configured with any programming language or tool that supports making REST calls, or with the EdgeCmd utility. For more information, see the [EdgeCmd utility documentation (https://osisoft.github.io/Edgecmd-Docs/content/edgecmd-utility.html)](https://osisoft.github.io/Edgecmd-Docs/content/edgecmd-utility.html). To validate successful configurations, you can perform data retrieval (GET commands) using a browser, if available on your device.
=======
The examples in the configuration topics use `curl`, a commonly available tool on both Windows and Linux. You can configure the adapter with any programming language or tool that supports making REST calls, or with the EdgeCmd utility. For more information, see the [EdgeCmd utility documentation](https://docs.osisoft.com/bundle/edgecmd/page/index.html). To validate successful configurations, you can perform data retrieval (GET commands) using a browser, if available on your device.
>>>>>>> 4058395b (fixing broken xref)

For more information on PI Adapter configuration tools, see [Configuration tools](xref:ConfigurationTools).

## Quick start

This Quick Start guides you through setup of each configuration file available for PI Adapter for BACnet. As you complete each step, perform each required configuration to establish a data flow from a data source to one or more endpoints. Some configurations are optional.

**Important:** If you want to complete the optional configurations, complete those tasks before the required tasks.

1. Configure one or several BACnet system components.

    See <xref:SystemComponentsConfiguration>.

1. Configure a BACnet data source for each BACnet device.

    See <xref:PIAdapterforBACnetDataSourceConfiguration>.

1. **Optional**: Configure schedules.

    See <xref:SchedulesConfiguration>.

1. Configure a BACnet data selection for each BACnet data source.

    See <xref:PIAdapterforBACnetDataSelectionConfiguration>.

1. **Optional**: Configure data filters, diagnostics and metadata, buffering, and logging.

    See the following topics:

    - <xref:DataFiltersConfiguration>
    - <xref:GeneralConfiguration>
    - <xref:BufferingConfiguration>
    - <xref:LoggingConfiguration><br/><br/>

1. Configure one or more egress and health endpoints. If there is a proxy between the adapter and your egress endpoints, define it.

    See the following topics:

    - <xref:EgressEndpointsConfiguration>
    - <xref:ConfigureANetworkProxy>
    - <xref:HealthEndpointConfiguration>
