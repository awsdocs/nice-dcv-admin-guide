# Changing the NICE DCV Server TCP/UDP ports and listen address<a name="manage-port-addr"></a>

By default, the NICE DCV server is configured to listen on TCP port `8443` and to communicate on any of the network interfaces on the host it runs on\.

You can specify a custom TCP port after you installed the NICE DCV server\. If you configured the NICE DCV server to [enable QUIC](enable-quic.md), you can also specify a custom UDP port for the QUIC traffic\. The port numbers must be higher than 1024\.

You can specify the network address the NICE DCV server listens on\. For instance, this allows you to specify whether only IPv4 or IPv6 should be used\. It also allows you to bind the server to a specific network interface and ensure that the traffic flows through a specific network\.

**Important**  
Whenever you apply changes to the network configuration of NICE DCV server, ensure that you communicate the changes to your clients, for instance they need to know the port number used to connect to sessions\.

**Tip**  
An alternative approach to control the network address and ports exposed to your clients consists in using the [NICE DCV Connection Gateway](https://docs.aws.amazon.com/dcv/latest/gw-admin/what-is-gw.html) or another web proxy or load balancer as a frontend to your servers\. Accessing your NICE DCV server hosts through a gateway allows you to have a single address for your servers\. It also allows to use port numbers lower than 1024, including 443, the standard port number for HTTPS\.  
Refer to the documentation of your gateway for more information about configuiring its network address and ports\.

**Topics**
+ [Changing the server TCP/UDP ports](#manage-ports)
+ [Listening on specific endpoints](#manage-listen-endpoints)

## Changing the NICE DCV server TCP/UDP ports<a name="manage-ports"></a>

------
#### [ Windows NICE DCV server ]

To change the ports that are used by the NICE DCV server, configure the `web-port` and the `quic-port` parameters using the Windows Registry Editor\.

**To change the ports for the server on Windows**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key\.

1. To configure the TCP port, select the **web\-port** parameter\.

   If there's no `web-port` parameter in the registry key, create one:

   1. In the navigation pane, open the context \(right\-click\) menu for the **connectivity** key\. Then, choose **New**, **DWORD \(32\-bit\) value**\.

   1. For **Name**, enter `web-port` and press **Enter**\.

1. Open the **web\-port** parameter\. For **Value data**, enter the new TCP port number\. If you don't configure this parameter, the NICE DCV server uses TCP port 8443 by default\.
**Note**  
The TCP port number must be higher than 1024\.

1. If QUIC is eanabled, to configure the UDP port, select the **quic\-port** parameter\.

   If there's no `quic-port` parameter in the registry key, create one:

   1. In the navigation pane, open the context \(right\-click\) menu for the **connectivity** key\. Then, choose **New**, **DWORD \(32\-bit\) value**\.

   1. For **Name**, enter `quic-port` and press **Enter**\.

1. Open the **quic\-port** parameter\. For **Value data**, enter the new UDP port number\. If you don't configure this parameter and QUIC support is enabled, the NICE DCV server uses UDP port 8443 by default\.
**Note**  
The UDP port number must be higher than 1024\.

1. Choose **OK** and close the Windows Registry Editor\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------
#### [ Linux NICE DCV server ]

To change the ports that are used by the NICE DCV server, configure the `web-port` and the `quic-port` parameters in the `dcv.conf` file\.

**To change the ports for the server on Linux**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `web-port` parameter in the `[connectivity]` section\. Then, replace the existing TCP port number with the new TCP port number\.

   If there's no `web-port` parameter in the `[connectivity]` section, add it manually using the following format:

   ```
   [connectivity]
   web-port=port_number
   ```
**Note**  
The TCP port number must be higher than 1024\.

1. Locate the `quic-port` parameter in the `[connectivity]` section\. Then, replace the existing UDP port number with the new UDP port number\.

   If there's no `web-port` parameter in the `[connectivity]` section, add it manually using the following format:

   ```
   [connectivity]
   quic-port=port_number
   ```
**Note**  
The UDP port number must be higher than 1024\.

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------

## Listening on specific endpoints<a name="manage-listen-endpoints"></a>

To listen only on specific network addresses, you can set the `web-listen-endpoints` and the `quic-listen-endpoints` parameters in the configuration of the NICE DCV server\.

Each endpoint is represented by an IPv4 or IPv6 address, optionally followed by a port number separated by `:`\. The port number specified in the endpoint takes priority over the ports specified in the `web-port` and `quic-port` parameters\.

Since it is possible to specify more than one endpoint, a set of endpoints is represented by a comma\-separated list, enclosed in square brackets, where each endpoint is between single quotation marks\. For example, `['0.0.0.0:8443', '[::]:8443']` represents any local IPv4 address and any local IPv6 address, both on port 8443, `'[::%1]:8443'` represents the IPv6 address which is bound to the network interface with index 1 on a Windows host, `'[::%eth1]:8443'` represents the IPv6 address which is bound to the `eth1` network interface on a Linux host\.

**Note**  
These configuration parameters are only available starting from NICE DCV Server 2022\.0\.

------
#### [ Windows NICE DCV server ]

**To change the endpoints for the server on Windows**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key\.

1. To configure the TCP endpoints, select the **web\-listen\-endpoints** parameter\.

   If there's no `web-listen-endpoints` parameter in the registry key, create one:

   1. In the navigation pane, open the context \(right\-click\) menu for the **connectivity** key\. Then, choose **New**, **String value**\.

   1. For **Name**, enter `web-listen-endpoints` and press **Enter**\.

1. Open the **web\-listen\-endpoints** parameter\. For **Value data**, enter a list of endpoints\.

1. If QUIC is enabled, to configure the UDP endpoints, select the **quic\-listen\-endpoints** parameter\.

   If there's no `quic-listen-endpoints` parameter in the registry key, create one:

   1. In the navigation pane, open the context \(right\-click\) menu for the **connectivity** key\. Then, choose **New**, **String value**\.

   1. For **Name**, enter `quic-listen-endpoints` and press **Enter**\.

1. Open the **quic\-listen\-endpoints** parameter\. For **Value data**, enter a list of endpoints\.

1. Choose **OK** and close the Windows Registry Editor\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------
#### [ Linux NICE DCV server ]

**To change the endpoints for the server on Linux**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `web-listen-endpoints` parameter in the `[connectivity]` section\. Then, replace the existing list of endpoints\.

   If there's no `web-listen-endpoints` parameter in the `[connectivity]` section, add it manually using the following format:

   ```
   [connectivity]
   web-listen-endpoints=[endpoint1, endpoint2]
   ```

1. Locate the `quic-listen-endpoints` parameter in the `[connectivity]` section\. Then, replace the existing list of endpoints\.

   If there's no `quic-listen-endpoints` parameter in the `[connectivity]` section, add it manually using the following format:

   ```
   [connectivity]
   quic-listen-endpoints=[endpoint1, endpoint2]
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------