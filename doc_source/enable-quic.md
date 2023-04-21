# Enabling the QUIC UDP transport protocol<a name="enable-quic"></a>

By default, NICE DCV uses the WebSocket protocol, which is based on TCP, for data transport\.

You can configure NICE DCV to use the QUIC protocol for data transport\. This transport protocol is based on UDP\. If your network experiences high latency and packet loss, using QUIC might improve performance\. If you enable QUIC, the NICE DCV server uses the QUIC protocol for data transport\. However, it continues to use WebSocket for authentication traffic\.

**Note**  
You can use QUIC only if UDP traffic is permitted by your network and security configuration\.

If you enable QUIC, clients can use the QUIC protocol for transporting data when connecting to a NICE DCV server session\. If clients don't use the QUIC protocol when they connect, they use WebSocket\. For more information about the QUIC protocol, see [ Connecting to a NICE DCV Session](https://docs.aws.amazon.com/dcv/latest/userguide/using-connecting.html) in the *NICE DCV User Guide*\.

------
#### [ Windows NICE DCV server ]

**To configure NICE DCV to use QUIC \(UDP\) for data transport**

1. Open the Windows Registry Editor and navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key\.

1. Open the **enable\-quic\-frontend** parameter\. For **Value data**, enter `1`\.
**Note**  
If you can't find the parameter, create a new DWORD \(32\-bit\) parameter and name it `enable-quic-frontend`\.

1. Close the Windows Registry Editor\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------
#### [ Linux NICE DCV server ]

**To configure NICE DCV to use QUIC \(UDP\) for data transport**

1. Open `/etc/dcv/dcv.conf` with your preferred text editor\.

1. In the `[connectivity]` section, do the following:
   + For `enable-quic-frontend`, specify `true`\.

   ```
   [connectivity]
   enable-quic-frontend=true
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------