---
uid: LoggingConfiguration
---

# Logging configuration

OSIsoft adapters write daily log messages for the adapter, the system, and omf egress to flat text files in the following locations:

• Windows: *%ProgramData%\OSIsoft\Adapters\adapterName\adapterId\Logs*

• Linux: */usr/share/OSIsoft/Adapters/adapterName/adapterId/Logs*

Each message in the log displays the message severity level, timestamp, and the message itself.

## Configure logging

Complete the following procedure to change the logging configuration: 

1. Using any text editor, create a file that contains the logging configuration in JSON form.
    - For content structure, see [Example Default logging configuration](#example-default-logging-configuration).
    - For all available parameters, see [Logging parameters](#logging-parameters).
 
2. Save the file, for example as *Component_Logging.json*.

3. Use any of the [Configuration tools](xref:ConfigurationTools) capable of making HTTP requests to execute a PUT command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/<ComponentId>/Logging`.

    **Note:**  Replace _&lt;ComponentId&gt;_ with the ComponentId of the adapter, for example _OpcUa1_.

    Example using curl (run this command from the same directory where the file is located):

    ```bash
    curl -d "@Component_Logging.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/<ComponentId>/Logging"
    ```
    
On successful execution, the log level change takes effect immediately during runtime. The other configurations (log file size and file count) get updated after the adapter is restarted. 

**Note:**  Any parameter not specified in the updated configuration file will revert to the default schema value.

## Logging schema

The full schema definition for the logging configuration is in the component specific logging file: _AdapterName_Logging_schema.json_, _OmfEgress_Logging_schema.json_, or _System_Logging_schema.json_ here:

Windows: *%ProgramFiles%\OSIsoft\Adapters\AdapterName\Schemas*

Linux: */opt/OSIsoft/Adapters/AdapterName/Schemas*

## Logging parameters

The following parameters are available for configuring logging:

| Parameter                | Required | Type      | Description |
| ------------------------ | -------- | --------- | ----------- |
|**logLevel**              | Optional | reference | The logLevel sets the minimum severity for messages to be included in the logs. Messages with a severity below the level set are not included. The log levels in their increasing order of severity are as follows: Trace, Debug, Information, Warning, Error, Critical. For detailed information about the logLevels, see [LogLevel](#loglevel). |
|**logFileSizeLimitBytes** | Optional | `integer` | The maximum size in bytes of log files that the service will create for the component. It must be a positive integer.|
|**logFileCountLimit**     | Optional | `integer` | The maximum number of log files that the service will create for the component. It must be a positive integer.|

### LogLevel

| Level       | Description                         |
|-------------|-------------------------------------|
| Trace         | Logs that contain the most detailed messages. These messages may contain sensitive application data like actual received values, which is why these messages shouldn’t be enabled in production environment. |
| Debug | Logs that can be used to troubleshoot data flow issues by recording metrics and detailed flow related information. |
| Information | Logs that track the general flow of the application. Any non-repetitive general information (like version information relating to the software at startup, what external services are being used, data source connection string, number of measurements, egress URL, change of state “Starting”, “Stopping”, or configuration) can be useful for diagnosing potential application errors.  |
| Warning | Logs that highlight an abnormal or unexpected event in the application flow, but does not otherwise cause the application execution to stop. Warning messages can indicate an unconfigured data source state, that a communication with backup failover instance has been lost, an insecure communication channel in use, or any other event that could require attention, but that does not impact data flow. |
| Error | Logs that highlight when the current flow of execution is stopped due to a failure. These should indicate a failure in the current activity, not an application-wide failure. This can indicate an invalid configuration, unavailable external endpoint, internal flow error, and so on.|
| Critical | Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention. This can indicate application wide failures like beta timeout expired, unable to start self-hosted endpoint, unable to access vital resource (for example, Data Protection key file), and so on. |


## Example Default logging configuration

By default, logging captures Information, Warning, Error, and Critical messages in the message logs.
The following logging configuration is the default for a component on install:

```json
{
  "logLevel": "Information",
  "logFileSizeLimitBytes": 34636833,
  "logFileCountLimit": 31   
}
```

## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/System/Logging | GET | Retrieves the system logging configuration
| api/v1/configuration/System/Logging | PUT | Updates the system logging configuration 
| api/v1/configuration/_ComponentId_/Logging | GET | Retrieves the logging configuration of the specified adapter component
| api/v1/configuration/_ComponentId_/Logging | PUT | Updates the logging configuration of the specified adapter component

**Note:** Replace *ComponentId* with the Id of your adapter component, for example Modbus1 or OpcUa1.
