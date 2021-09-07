# Enable the QUIC UDP transport protocol<a name="enable-quic"></a>

By default, NICE DCV uses the WebSocket protocol, which is based on TCP, for data transport\.

You can configure NICE DCV to use the QUIC transport protocol, which is based on UDP, for data transport\. Using QUIC can improve performance if your network experiences high latency and packet loss\. If you enable QUIC, the NICE DCV server uses the QUIC protocol for data transport, but it continues to use WebSocket for authentication traffic\.

**Note**  
You can only use QUIC if your network and security configuration allows UDP traffic\.

If you enable QUIC, clients can choose to use the QUIC protocol for transporting data when connecting to a session on the NICE DCV server\. If clients don't choose the QUIC protocol when they connect, they will use WebSocket\. For more information about choosing the QUIC protocol when connecting to a session, see [ Connecting to a NICE DCV Session](https://docs.aws.amazon.com/dcv/latest/userguide/using-connecting.html) in the *NICE DCV User Guide*\.

------
#### [ Windows NICE DCV server ]

**To configure NICE DCV to use QUIC \(UDP\) for data transport**

1. Open the Windows Registry Editor and navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key\.

1. Open the **enable\-quic\-frontend** parameter\. For **Value data**, enter `1`\.
**Note**  
If the parameter doesn't exist, create a new DWORD \(32\-bit\) parameter and name it `enable-quic-frontend`\.

1. \(Optional\) Open the **quic\-port** parameter\. For **Value data**, enter the port to use for QUIC traffic\. If you don't configure this parameter, the NICE DCV server uses port 8443 by default\.
**Note**  
If the parameter doesn't exist, create a new DWORD \(32\-bit\) parameter and name it `quic-port`\.

1. \(Optional\) Open the **web\-port** parameter\. For **Value data**, enter the port to use for WebSocket \(TCP\) traffic\. If you don't configure this parameter, the NICE DCV server uses port 8443 by default\.
**Note**  
If the parameter doesn't exist, create a new DWORD \(32\-bit\) parameter and name it `web-port`\.

1. Close the Windows Registry Editor\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------
#### [ Linux NICE DCV server ]

**To configure NICE DCV to use QUIC \(UDP\) for data transport**

1. Open `/etc/dcv/dcv.conf` with your preferred text editor\.

1. In the `[connectivity]` section, do the following:
   + For `enable-quic-frontend`, specify `true`\.
   + \(Optional\) For `quic-port`, enter the port to use for QUIC traffic\. If you don't configure this parameter, the NICE DCV server uses port 8443 by default\.
   + \(Optional\) For `web-port`, enter the port to use for WebSocket \(TCP\) traffic\. If you don't configure this parameter, the NICE DCV server uses port 8443 by default\. 

   For example:

   ```
   [connectivity]
   enable-quic-frontend=true
   quic-port=port_number
   web-port=port_number
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------