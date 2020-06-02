---
uid: BACnetPolledDataStreamConfiguration
---

# Polled data stream configuration

## Overview

Polled data collection is the default data collection mode for the adapter. Under this mode of data collection, devices configured for polling will be requested at scheduled intervals for all properties whose data selection items have a DataCollectionMode of Poll. To avoid overloading the network, requests are limited via the MaxConcurrentNetworkRequests property on the Data Selection configuration. However, Change of Value (CoV) is generally preferred when supported by the configured device, as data values will only be sent when they change instead of every time the scheduled interval elapses.

## Usage
For a given Data Selection Item, omitting the DataCollectionMode or specifying a DataCollectionMode of Poll will cause the selected property to be polled at the scheduled interval. 
