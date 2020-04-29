---
uid: StartAndStopAnAdapter
---

# Start and stop an adapter

Complete one of the following procedures for your operating system to start or stop an adapter service:

## Windows

1. Open Windows services.

2. Select **OSIsoft Adapter for _AdapterName_**, for example OSIsoft Adapter for Modbus.

3. Depending on whether your adapter is running or not, click either **Start** or **Stop**.

## Linux

1. Open command line.

2. Depending on whether your adapter is running or not, type one of the following:

    Example: **Start** OSIsoft Adapter for OPC UA

    ```cmdline
    systemctl start OSIsoft Adapter for OPC UA
    ```

    Example: **Stop** OSIsoft Adapter for Modbus TCP

    ```cmdline
    systemctl stop OSIsoft Adapter for Modbus
    ```
  
3. Press Enter.

