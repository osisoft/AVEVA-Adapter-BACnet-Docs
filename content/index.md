---
uid: PIAdapterforBACnetOverview
---

# Overview

PI Adapter for BACnet is a data-collection component that transfers time-series data from source devices to OMF endpoints in OSIsoft Cloud Services or PI Servers. Building Automation and Control Networks (BACnet) is a communication protocol that is developed and maintained by ASHRAE. The adapter adheres to ANSI/ASHRAE Standard 135-2012 and communicates with any device using BACnet/IP and devices that conform to other BACnet protocols using a BACnet gateway or router.

![PI Adapter for BACnet architecture](images/pi-adapter-for-bacnet-architecture-diagram.png)

## Adapter installation

You can install the adapter with a download kit that you can obtain from the OSIsoft Customer Portal. You can install the adapter on devices running either Windows or Linux operating systems.

## Adapter configuration

Using REST API, you can configure all functions of the adapter. The configurations are stored in JSON files. For data ingress, you must define an adapter component in the system components configuration for each data source to which the adapter will connect. You configure each adapter component with the connection information for the data source and the data to collect. For data egress, you must specify destinations for the data, including security for the outgoing connection. Additional configurations are available to egress health and diagnostics data, add buffering configuration to protect against data loss, and record logging information for troubleshooting purposes.

After you have configured the adapter and it is sending data, you can use administration functions to manage the adapter or individual ingress components of the adapter. Health and diagnostics functions monitor the status of connected devices, adapter system functions, the number of active data streams, the rate of data ingress, the rate of errors, and the rate of data egress.

## EdgeCmd utility

OSIsoft provides the EdgeCmd utility, a proprietary command line tool to configure and administer an adapter on both Linux and Windows operating systems. EdgeCmd utility is installed separately from the adapter.
