---
uid: InstallPIAdapterForBACnetUsingDocker
---

# Install PI Adapter for BACnet using Docker

Docker is a set of tools that can be used on Linux to manage application deployments. 

**Note:** If you want to use Docker, you must be familiar with the underlying technology and have determined that it is appropriate for your planned use of the BACnet Adapter. Docker is not a requirement to use adapter.

This topic provides examples of how to create a Docker container with the BACnet Adapter. 

## Create a startup script for the Adapter

1. Using the text editor, create a script similar to the following.

	**Note:** The script varies slightly by processor.

	**ARM32**

	```bash
	#!/bin/sh
	#local variables
	defaultPort=5590
	#regexp to only accept numerals
	re='^[0-9]+$'
	
	portConfigFile="/BACnet_linux-arm/appsettings.json"

	#validate the port number input
	if [ -z $portnum ] ; then
			portnum=${defaultPort} 
			echo "Default value selected." ;
	else
			echo $portnum | grep -q -E $re
			isNum=$?
			if [ $isNum -ne 0 ] || [ $portnum -le 1023 ] || [ $portnum -gt 49151 ] ; then
					echo "Invalid input. Setting default value ${defaultPort} instead..."
					portnum=${defaultPort} ;
			fi
	fi

	echo "configuring port ${portnum}"
	#write out the port config file
	cat > ${portConfigFile} << EOF
	{
	"ApplicationSettings": {
			"Port": ${portnum},
			"ApplicationDataDirectory": "/usr/share/OSIsoft/Adapters/BACnet"
			}
	}
	EOF
	exec /BACnet_linux-arm/OSIsoft.Data.System.Host
	```

	**ARM64**

	```bash
	#!/bin/sh
	#local variables
	defaultPort=5590
	#regexp to only accept numerals
	re='^[0-9]+$'
	
	portConfigFile="/BACnet_linux-arm64/appsettings.json"

	#validate the port number input
	if [ -z $portnum ] ; then
			portnum=${defaultPort} 
			echo "Default value selected." ;
	else
			echo $portnum | grep -q -E $re
			isNum=$?
			if [ $isNum -ne 0 ] || [ $portnum -le 1023 ] || [ $portnum -gt 49151 ] ; then
				echo "Invalid input. Setting default value ${defaultPort} instead..."
				portnum=${defaultPort} ;
			fi
	fi

	echo "configuring port ${portnum}"
	#write out the port config file
	cat > ${portConfigFile} << EOF
	{
	"ApplicationSettings": {
			"Port": ${portnum},
			"ApplicationDataDirectory": "/usr/share/OSIsoft/Adapters/BACnet"
			}
	}
	EOF
	exec /BACnet_linux-arm64/OSIsoft.Data.System.Host
	```

	**AMD64**

	```bash
	#!/bin/sh
	#local variables
	defaultPort=5590
	#regexp to only accept numerals
	re='^[0-9]+$'
	
	portConfigFile="/BACnet_linux-x64/appsettings.json"

	#validate the port number input
	if [ -z $portnum ] ; then
			portnum=${defaultPort} 
			echo "Default value selected." ;
	else
			echo $portnum | grep -q -E $re
			isNum=$?
			if [ $isNum -ne 0 ] || [ $portnum -le 1023 ] || [ $portnum -gt 49151 ] ; then
					echo "Invalid input. Setting default value ${defaultPort} instead..."
					portnum=${defaultPort} ;
			fi
	fi

	echo "configuring port ${portnum}"
	#write out the port config file
	cat > ${portConfigFile} << EOF
	{
	"ApplicationSettings": {
			"Port": ${portnum},
			"ApplicationDataDirectory": "/usr/share/OSIsoft/Adapters/BACnet"
			}
	}
	EOF
	exec /BACnet_linux-x64/OSIsoft.Data.System.Host
	```
	
2. Name the script *bacnetdockerstart.sh* and save it to the directory where you plan to create the container.

## Create a Docker container containing the BACnet Adapter

1. Create the following `Dockerfile` in the directory where you want to create and run the container.

	**Note:** `Dockerfile` is the required name of the file. Use the variation according to your operating system:

	### ARM32

	```bash
	FROM ubuntu
	WORKDIR /
	RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends libicu60 libssl1.0.0
	COPY bacnetdockerstart.sh /
	RUN chmod +x /bacnetdockerstart.sh
	ADD ./BACnet_linux-arm.tar.gz .
	ENTRYPOINT ["/bacnetdockerstart.sh"]
	```

	### ARM64

	```bash
	FROM ubuntu
	WORKDIR /
	RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends libicu60 libssl1.0.0
	COPY bacnetdockerstart.sh /
	RUN chmod +x /bacnetdockerstart.sh
	ADD ./BACnet_linux-arm64.tar.gz .
	ENTRYPOINT ["/bacnetdockerstart.sh"]
	```

	### AMD64 (x64)

	```bash
	FROM ubuntu
	WORKDIR /
	RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends libicu60 libssl1.0.0
	COPY bacnetdockerstart.sh /
	RUN chmod +x /bacnetdockerstart.sh
	ADD ./BACnet_linux-x64.tar.gz .
	ENTRYPOINT ["/bacnetdockerstart.sh"]
	```

2. Copy the `BACnet_linux-\<platform>.tar.gz` file to the same directory as the `Dockerfile`.
3. Copy the `bacnetdockerstart.sh` script to the same directory as the `Dockerfile`.
4. Run the following command line in the same directory (`sudo` may be necessary):

	```bash
	docker build -t bacnetadapter .
	```

## Run the BACnet Adapter Docker container

### REST access from the local host to the Docker container

Complete the following to run the container:

1. Open the docker container `bacnetadapter` previously created.
2. Type the following in the command line (`sudo` may be necessary):

	```bash
	docker run -d --network host bacnetadapter
	```

Port `5590` is accessible from the host and you can make REST calls to BACnet Adapter from applications on the local host computer. In this example, all data stored by the BACnet Adapter is stored in the container itself. When the container is deleted, the data stored is also deleted.

### Persistent storage on the local file system from Docker

Complete the following to run the container:

1. Use the docker container image `bacnetadapter` previously created.
2. Type the following in the command line (`sudo` may be necessary):

	```bash
	docker run -d --network host -v /bacnet:/usr/share/OSIsoft/ bacnetadapter
	```

Port `5590` is accessible from the host and you can make REST calls to the BACnet Adapter from applications on the local host computer. In this example, all data that would be written to the container is instead written to the host directory and the host directory is a directory on the local machine, /bacnet. You can specify any directory.

### Port number change

To use a different port other than `5590` you can specify a `portnum` variable on the `docker run` command line. For example, to 
start the adapter using port `6000` instead of `5590`, use the command line:

```bash
docker run -d -e portnum=6000 --network host bacnetadapter
```

This command accesses the REST API with port `6000` instead of port `5590`. The following `curl` command returns the configuration for the container.

```bash
curl http://localhost:6000/api/v1/configuration
```

### Remove REST access to the Docker container

If you remove the `--network host` option from the docker run command, REST access is not possible from outside the container. This may be valuable when you want to host an application in the same container as BACnet Adapter, but do not want to have external REST access enabled.
