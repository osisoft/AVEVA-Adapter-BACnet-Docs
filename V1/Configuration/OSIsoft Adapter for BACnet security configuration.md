---
uid: OSIsoftAdapterforBACnetSecurityConfiguration
---

# OSIsoft Adapter for BACnet security configuration

The BACnet security standard is concerned with the authentication of client and server applications, the authentication of users and confidentiality of their communication. As the security model relies heavily on Transport Level Security (TLS) to establish a secure communication link with an BACnet server, each client, including the OSIsoft adapter, must have a digital certificate deployed and configured. Certificates uniquely identify client applications and machines on servers, and allow for creation of a secure communication link when trusted on both sides.

BACnet adapter generates a self-signed certificate when the first secure connection attempt is made. Each BACnet adapter instance creates a certificate store where its own certificates, as well as those of the server, will be persisted.

## Configure BACnet adapter security

Complete the following procedure to configure BACnet adapter security:

1. In your data source configuration, set `UseSecureConnection` to **true**. For more information, see [OSIsoft Adapter for BACnet data source configuration](xref:OSIsoftAdapterforBACnetDataSourceConfiguration).

   The adapter verifies whether the server certificate is present in the [adapter trusted certificates](#adapter-trusted-certificates) folder and is therefore trusted. In case the certificates were not exchanged before the first attemped connection, the adapter persists the server certificate within the [adapter rejected certificates](#adapter-rejected-certificates) folder and the following warning message about the rejected server certificate will be printed:

   ```bash
   ~~2019-09-08 11:45:48.093 +01:00~~ [Warning] Rejected Certificate: "DC=MyServer.MyDomain.int, O=Prosys BACnet, CN=Simulation
   ```

2. Manually move the server certificate from the [_RejectedCertificates\certs_](#adapter-rejected-certificates) folder to the [_Trusted\certs_](#adapter-trusted-certificates) folder using a file explorer or command-line interpreter.

   Linux example using command-line:

   ```bash
   mv /usr/share/OSIsoft/Adapters/BACnet/BACnet1/Certificates/RejectedCertificates/certsSimulationServer\ \[F9823DCF607063DBCECCF6F8F39FD2584F46AEBB\].der /usr/share/OSIsoft/Adapters/BACnet/BACnet1/Certificates/Trusted/certs/
   ```

   **Note:** Administrator or root privileges are required to perform this operation.

   Once the certificate is in the adapter trusted certificates folder, the adapter trusts the server and the connection attempt proceeds in making the connection call to the configured server.
  
3. Add the [certificate of the adapter](#certificate-of-the-adapter) to the server's trust store.

   The connection succeeds only when the adapter certificate is trusted on the server side. For more details on how to make a client certificate trusted, see your BACnet server documentation. In general, servers work in a similar fashion as the clients, hence you can take a similar approach for making the server certificate trusted on the client side.
   
   When certificates are mutually trusted, the connection attempt succeeds and the adapter is connected to the most secure endpoint provided by the server.

### Certificate locations

#### Adapter rejected certificates

Windows: `%programdata%\OSIsoft\Adapters\BACnet\{ComponentId}\Certificates\RejectedCertificates\certs`

Linux: `/usr/share/OSIsoft/Adapters/BACnet/{ComponentId}/Certificates/RejectedCertificates/certs`


#### Adapter trusted certificates

Windows: `%programdata%\OSIsoft\Adapters\BACnet\{ComponentId}\Certificates\Trusted\certs`

Linux: `/usr/share/OSIsoft/Adapters/BACnet/{ComponentId}/Certificates/Trusted/certs`


#### Certificate of the adapter

Windows: `%programdata%\OSIsoft\Adapters\BACnet\{ComponentId}\Certificates\My\certs`

Linux: `/usr/share/OSIsoft/Adapters/BACnet/{ComponentId}/Certificates\My\certs`

