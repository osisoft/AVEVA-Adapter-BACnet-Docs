

# Data Packet Tracing 

Data packet tracing is a configurable feature that logs all incoming and outgoing UDP packet data to the adapter component log.


## Enable Packet Tracing

To enable tracing, set the adapter component log-level to Trace. See [Logging Configuration](xref:LoggingConfiguration)


## Example Log

```
2020-07-28 11:14:25.513 -07:00 [Verbose] Sent bytes: 
81 0a 00 1b 01 24 00 14 06 01 00 00 00 00 00 ff 
02 75 01 0c 0c 02 00 00 01 19 3e 
2020-07-28 11:14:25.599 -07:00 [Verbose] Received bytes: 
81 0a 00 1e 01 08 00 14 06 01 00 00 00 00 00 30 
01 0c 0c 02 00 00 01 19 3e 3e 22 04 00 3f 
```

