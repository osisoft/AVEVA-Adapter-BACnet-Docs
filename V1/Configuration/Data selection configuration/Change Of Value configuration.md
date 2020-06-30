---
uid: BACnetCOVConfiguration
---

# Change Of Value (COV) configuration

## Overview

COV or Change of Value is one of two available data collection modes for the adapter. For supported BACnet devices (i.e. for devices whose Device Configuration's ServicesSupported includes SubscribeCov and/or SubscribeCovProperty) users can choose to enable COV mode. COV is a subscription-based data collection mode, where the device will "push" new data when the value changes by more than the subscription's designated amount. COV is generally preferred when available, as it tends to improve performance and decrease network usage.

## Usage 

To enable COV for a specified data selection item, change the DataCollectionMode to SubscribeCov or SubscribeCovProperty. In SubscribeCovProperty mode, an optional CovIncrement can also be specified on the data selection item to specify a minimum amount that the value must change in order to prompt the new value to be sent. While COV mode is enabled, it is advised that at least one data selection item be configured in polled data collection mode per device in order to maintain an accurate device status.
