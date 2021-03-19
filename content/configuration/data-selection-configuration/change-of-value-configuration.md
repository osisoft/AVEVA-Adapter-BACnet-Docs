---
uid: BACnetCOVConfiguration
---

# COV (Change Of Value) configuration


## Usage

To enable COV for a specified data selection item, change the DataCollectionMode to `SubscribeCov` or `SubscribeCovProperty` in data selection configuration. The configured schedule will determine how often the adapter attempts to resubscribe the item for COV notifications. If you do not configure a schedule, the item will not be subscribed.

In `SubscribeCov` mode, the adapter subscribes to a BACnet object on the device, and the device reports values on change for properties enabled for COV reporting based on object type, typically including `PresentValue` and `StatusFlags`. If the data selection item **PropertyIdentifier** is specified, it must match one of these properties, otherwise COV notifications for this item will not be written to the data stream. If **PropertyIdentifier** is omitted, `PresentValue` will be used for the stream.

In `SubscribeCovProperty` mode, the adapter subscribes to a unique BACnet object and property combination on the device. An optional `CovIncrement` can also be specified on the data selection item to specify a minimum amount that the value must change in order to prompt the new value to be sent. 

While COV mode is enabled, it is advised that at least one data selection item is configured in polled data collection mode per device in order to maintain an accurate device status.
