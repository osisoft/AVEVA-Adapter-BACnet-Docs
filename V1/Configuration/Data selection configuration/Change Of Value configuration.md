---
uid: BACnetCOVConfiguration
---

# Change Of Value (COV) configuration

## Overview

COV(Change of Value) is a subscription-based data collection method. For COV-compatible BACnet devices (i.e. for devices whose Device Configuration's ServicesSupported includes SubscribeCov and/or SubscribeCovProperty), users can choose to enable either SubscribeCov or SubscribeCovProperty data collection mode for the adapter, where the device will "push" new data when the value changes by more than the subscription's designated amount. COV is generally preferred when available, as it tends to improve performance and decrease network usage.

## Usage 

To enable COV for a specified data selection item, change the DataCollectionMode to SubscribeCov or SubscribeCovProperty in DataSelection configuration.

In SubscribeCov mode, the adapter subscribes to a BACnet object on the device, and the device reports values on change for properties enabled for COV reporting based on object type, typically including PresentValue and StatusFlags. In the data selection item, PropertyIdentifier, if specified, must match one of these properties, otherwise COV notifications for this item will not be written to the data stream. If PropertyIdentifier is ommitted, PresentValue will be used for the stream.

In SubscribeCovProperty mode, the adapter subscribes to a unique BACnet object and property combination on the device. An optional CovIncrement can also be specified on the data selection item to specify a minimum amount that the value must change in order to prompt the new value to be sent. 

While COV mode is enabled, it is advised that at least one data selection item be configured in polled data collection mode per device in order to maintain an accurate device status.