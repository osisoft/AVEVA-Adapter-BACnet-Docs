---
uid: InstallPIAdapterForBACnetUsingDocker
---

# Installation using Docker

Docker is a set of tools that you can use on Linux to manage application deployments. This topic provides examples of how to create a Docker container with the BACnet adapter.

**Note:** If you want to use Docker, you must be familiar with the underlying technology and have determined that it is appropriate for your planned use of the BACnet adapter. Docker is not a requirement to use the adapter.

## Create a startup script

To create a startup script for the adapter, follow the instructions below.

1. Use a text editor to create a script similar to one of the following examples:

    **Note:** The script varies slightly by processor.

    **ARM32**

    ```bash
    #!/bin/sh
    if [ -z $portnum ] ; then
        exec /BACnet_linux-arm/OSIsoft.Data.System.Host
    else
        exec /BACnet_linux-arm/OSIsoft.Data.System.Host --port:$portnum
    fi
    ```

    **ARM64**

    ```bash
    #!/bin/sh
    if [ -z $portnum ] ; then
        exec /BACnet_linux-arm64/OSIsoft.Data.System.Host
    else
        exec /BACnet_linux-arm64/OSIsoft.Data.System.Host --port:$portnum
    fi
    ```

    **AMD64**

    ```bash
    #!/bin/sh
    if [ -z $portnum ] ; then
        exec /BACnet_linux-x64/OSIsoft.Data.System.Host
    else
        exec /BACnet_linux-x64/OSIsoft.Data.System.Host --port:$portnum
    fi
    ```
 
2. Name the script `bacnetdockerstart.sh` and save it to the directory where you plan to create the container.

## Create a Dockerfile

To create a Docker file for the adapter, follow the instructions below.

1. Create the following `Dockerfile` in the directory where you want to create and run the container.

    **Note:** `Dockerfile` is the required name of the file. Use the variation according to your operating system:

    **ARM32**

    ```bash
    FROM ubuntu
    WORKDIR /
    RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y ca-certificates libicu60 libssl1.1 curl
    COPY bacnetdockerstart.sh /
    RUN chmod +x /bacnetdockerstart.sh
    ADD ./BACnet_linux-arm.tar.gz .
    ENTRYPOINT ["/bacnetdockerstart.sh"]
    ```

    **ARM64**

    ```bash
    FROM ubuntu
    WORKDIR /
    RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y ca-certificates libicu66 libssl1.1 curl
    COPY bacnetdockerstart.sh /
    RUN chmod +x /bacnetdockerstart.sh
    ADD ./BACnet_linux-arm64.tar.gz .
    ENTRYPOINT ["/bacnetdockerstart.sh"]
    ```

    **AMD64 (x64)**

    ```bash
    FROM ubuntu
    WORKDIR /
    RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y ca-certificates libicu66 libssl1.1 curl
    COPY bacnetdockerstart.sh /
    RUN chmod +x /bacnetdockerstart.sh
    ADD ./BACnet_linux-x64.tar.gz .
    ENTRYPOINT ["/bacnetdockerstart.sh"]
    ```

2. Copy the `BACnet_linux-\<platform>.tar.gz` file to the same directory as the `Dockerfile`.

3. Copy the `bacnetdockerstart.sh` script to the same directory as the `Dockerfile`.

4. Run the following command line in the same directory (you may need to use the `sudo` command):

    ```bash
    docker build -t bacnetadapter .
    ```

## Create a Docker container

The following procedures contain instructions on how to run the adapter inside a Docker container with different options enabled.

### Run the Docker container with REST access enabled

To run the adapter inside a Docker container with access to its REST API from the local host, complete the following steps:

1. Use the docker container `bacnetadapter` that you created previously.
2. Type the following command line (you may need to use the `sudo` command):

    ```bash
    docker run -d --network host bacnetadapter
    ```

The default port `5590` is accessible from the host and you can make REST calls to BACnet adapter from applications on the local host computer. In this example, all data stored by the BACnet adapter is stored in the container itself. When the container is deleted, the data stored is also deleted.

### Run the Docker container with persistent storage

To run the adapter inside a Docker container while using the host for persistent storage, complete the following steps. This procedure also enables access to the adapter REST API from the local host.

1. Use the docker container image `bacnetadapter` created previously.
2. Type the following command line (you may need to use the `sudo` command):

    ```bash
    docker run -d --network host -v /bacnet:/usr/share/OSIsoft/ bacnetadapter
    ```

The default port `5590` is accessible from the host and you can make REST calls to the BACnet adapter from applications on the local host computer. In this example, the data is written to a host directory on the local machine `/bacnet` rather than the container. You can specify any directory.

### Change port number

To use a different port other than the default `5590`, you can specify a `portnum` variable on the `docker run` command line. For example, to start the BACnet adapter using port `6000` instead of `5590`, use the following command line:

```bash
docker run -d -e portnum=6000 --network host bacnetadapter
```

This command accesses the REST API with port `6000` instead of port `5590`. The following `curl` command returns the configuration for the container.

```bash
curl http://localhost:6000/api/v1/configuration
```

### Remove REST access

If you remove the `--network host` option from the docker run command, REST access is not possible from outside the container. This can be valuable when you want to host an application in the same container as the BACnet adapter but do not want to have external REST access enabled.
