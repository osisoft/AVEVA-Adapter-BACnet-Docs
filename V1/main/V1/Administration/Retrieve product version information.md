---
uid: RetrieveProductVersionInformation
---

# Retrieve product version information

The product version information includes the application version, the version of the underlying .NET Core Framework, and the operating system that the adapter is running on.

Complete the following procedure to retrieve the product version information of an OSIsoft adapter:

1. Start any configuration tool capable of making HTTP requests.
2. Execute a GET command to the following endpoint: `GET http://localhost:5590/api/v1/Diagnostics/ProductInformation`

   Result example:

    ```
    {
        "Application Version": "1.1.0.0",
        ".Net Core Version": ".NET Core 3.1.0",
        "Operating System": "Microsoft Windows 10.0.18362"
    }
    ```
