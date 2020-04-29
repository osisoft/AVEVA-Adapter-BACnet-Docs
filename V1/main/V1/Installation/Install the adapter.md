---
uid: InstallTheAdapter
---

# Install the adapter

Adapters can be installed on either a Windows or Linux operating system. Before installing the adapter, see the [Installation prerequisites](xref:Installation#installation-prerequisites) section to ensure your machine is properly configured to provide optimum adapter operation. 

## Windows

Complete the following procedure to install an OSIsoft adapter on Windows:

1. Download the Windows .msi file from the [OSIsoft Customer portal (https://customers.osisoft.com/s/products)](https://customers.osisoft.com/s/products).

    **Note:** Customer login credentials are required to access the portal.

2. Run the .msi file.
3. Follow the setup wizard. 
    
    You can change the installation folder or port number during setup. The default port number is 5590.

4. Optional: Run the following curl command, using the port number that you specified during installation, to verify the installation:
   ```
   curl http://localhost:5590/api/v1/configuration
   ```

    If you receive an error, wait a few seconds and try the script again. If the installation was successful, a JSON copy of the default system configuration is returned 


## Linux

Complete the following procedure to install an OSIsoft adapter on Linux:

1. Download the appropriate Linux distribution file from the [OSIsoft Customer portal (https://customers.osisoft.com/s/products)](https://customers.osisoft.com/s/products).

    **Note:** Customer login credentials are required to access the portal.

2. Open a terminal.
3. Run the sudo apt install command. 

    For example, to install the Linux ARM Debian package, run command. `sudo apt install ./Modbus_linux-arm.deb`. To install the Linux    x64 package, run command `sudo apt install ./Modbus_linux-x64.deb`.

4. Optional: Run the following curl command, using the port number that you specified during installation, to verify the installation: 
   ```
   curl http://localhost:5590/api/v1/configuration
   ```

    If you receive an error, wait a few seconds and try the script again. If the installation was successful, a JSON copy of the default system configuration is returned 
