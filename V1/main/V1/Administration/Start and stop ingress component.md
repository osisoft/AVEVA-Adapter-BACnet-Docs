---
uid: StartAndStopIngressComponent
---

# Start and stop ingress component

By default, all currently configured ingress components are started.

## Start an ingress component

Complete the following procedure to start an individual ingress component:

1. Start any configuration tool capable of making HTTP requests.
2. Execute a POST command to the following endpoint, replacing `<ingressComponentId>` with the ingress component that you want to start: `http://localhost:5590/api/v1/administration/<ingressComponentId>/Start`
    
    Example **Start the OpcUa1 ingress component** using curl:

    ```bash
    curl -d "" -X POST "http://localhost:5590/api/v1/Administration/OpcUa1/Start"
    ```

    An HTTP status 204 message indicates success.

## Stop an ingress component

Complete the following procedure to stop an individual ingress component:

1. Start any configuration tool capable of making HTTP requests.
2. Execute a POST command to the following endpoint, replacing `<ingressComponentId>` with the ingress component that you want to stop: `http://localhost:5590/api/v1/administration/<ingressComponentId>/Stop`

    Example **Stop the Modbus1 ingress component** using cURL:

    ```bash
    curl -d "" -X POST "http://localhost:5590/api/v1/Administration/Modbus1/Stop"
    ```

    An HTTP status 204 message indicates success.
