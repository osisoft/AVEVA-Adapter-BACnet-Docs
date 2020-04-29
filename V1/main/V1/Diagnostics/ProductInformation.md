---
uid: EdgeDataStoreDiagnostics-ProductInformation
---

# Product versions

In order to get the application version, the version of the underlying .NET Core Framework, and the operating system that the adapter is running on, you can make requests against the Diagnostics endpoint. 

- Run the following command:

    ```
    GET http://localhost:5595/api/v1/Diagnostics/ProductInformation
    ```

    Result example:

    ```
    {
        "Application Version": "1.1.0.0",
        ".Net Core Version": ".NET Core 3.1.0",
        "Operating System": "Microsoft Windows 10.0.18362"
    }
    ```
