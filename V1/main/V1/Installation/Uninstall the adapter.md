---
uid: UninstallTheAdapter
---

# Uninstall the adapter

Complete one of the following procedures for your operating system to uninstall an OSIsoft adapter:

## Windows

1. To remove the OSIsoft adapter program files from a Windows device, use the Windows Control Panel uninstall application process.

    **Note:** The configuration, data, and log files are not removed by the uninstall process.

2. Optional: To remove data, configuration and log files, remove the directory _%ProgramData%\OSIsoft\Adapters\AdapterName_.

    This will delete all data processed by the adapter in addition to configuration and log files.


## Linux

1. To remove OSIsoft adapter software from a Linux device, open a terminal window and run the following command:

    ```bash
    sudo apt remove osisoft.adapters.<AdapterName>
    ```

2. Optional: To remove data, configuration, and log files, remove the directory _/usr/share/OSIsoft/Adapters/AdapterName_.

    This will delete all data processed  by the adapter, in addition to configuration and log files.

    Alternatively, you can run the following command:

    ```bash
    sudo rm -r /usr/share/OSIsoft/Adapters/<AdapterName>
    ```
