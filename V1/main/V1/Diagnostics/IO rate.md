---
uid: IORate
---

# IO rate

The Diagnostics.Adapter.IORate dynamic type includes these values, which are logged in a stream with the id {componentid}.IORate. IO rate includes only sequential data collected from a data source.

| Type   | Property  | Description                                            	|
| ------ | --------- | -------------------------------------------------------	|
| **string** | timestamp | Timestamp of event                                    	|
| **double** | IORate    | 1-minute rolling average of data rate (streams/second)	|
