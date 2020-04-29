---
uid: SystemComponentsConfiguration
---

# System components configuration

OSIsoft adapters use JSON configuration files in a protected directory on Windows and Linux to store configuration that is read on startup. While the files are accessible to view, OSIsoft recommends that you use REST or the edgecmd command line tool for any changes you make to the files. As part of making adapters as secure as possible, any passwords or secrets that you configure are stored in encrypted form (with cryptographic key material stored separately in a secure location.) If you edit the files directly, the adapter may not work as expected.

> **Note:** You can edit any single component or facet of the system using REST, but also configure the system as a whole with a single REST call.

## Configure system components

The default _System_Components.json_ file for the System component contains the following information. The Egress component is required for this initial release for adapters to run.

```json
[
  {
    "ComponentId": "Egress",
    "ComponentType": "OmfEgress"
  }
]
```

 You can add additional components if you want, but only a single OmfEgress component is supported. 

1. To add a new component, create a JSON file with the ComponentId and ComponentType. The following example adds a Modbus TCP adapter. 

    > **Note:** A unique ComponentId is necessary for each component in the system. This example uses the ComponentId Modbus1 since it is the first Modbus TCP adapter:

    ```json
      {
        "ComponentId": "Modbus1",
        "ComponentType": "Modbus"
      }
    ```

2. Save the JSON in a file named _AddComponent.json_. 
3. From the same directory where the file exists, run the following curl script:

    ```bash
    curl -i -d "@AddComponent.json" -H "Content-Type: application/json" http://localhost:5595/api/v1/configuration/system/components
    ```

After the curl command completes successfully, you can configure or use the new component.

### Delete a component

 - To delete an existing component, run the following curl script:

    ```bash
	curl -X DELETE http://localhost:5595/api/v1/configuration/system/components/{ComponentId_To_Delete}/
    ```

	All the logs and configurations files for the deleted components will be moved to the corresponding _logs/Removed_ or _Configuration/Removed_ folder.
	
## System components schema

The following table defines the basic behavior of the _AddComponent.json_ file.

| Abstract            | Extensible | Status       | Identifiable | Custom properties | Additional properties |                           
| ------------------- | ---------- | ------------ | ------------ | ----------------- | --------------------- | 
| Can be instantiated | Yes        | Experimental | No           | Forbidden         | Forbidden             |


## Parameters for system components

The following parameters are available for configuring system components.

| Parameters     | Required | Type    | Nullable | Description |
| -------------- | -------- | --------| ---------|-------------|
| ComponentId    | Required |`string` | Yes      | The ID of the component. It can be any alphanumeric string, for example Egress.|
| ComponentType  | Required |`string` | Yes      | The type of the component, for example OmfEgress. There are two types of components: OmfEgress and the adapter. |

## System components example

```json
[
  {
                "componentId": "Modbus1",
                "componentType": "Modbus"
            },
            {
                "componentId": "Modbus2",
                "componentType": "Modbus"
            },
            {
                "ComponentId": "Egress",
                "ComponentType": "OmfEgress"
   }
]
```
