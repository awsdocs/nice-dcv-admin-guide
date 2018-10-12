# Configuring NICE DCV Authentication<a name="security-authentication"></a>

By default, clients are required to authenticate against the server on which NICE DCV is hosted before connecting to a NICE DCV session\. If the client fails to authenticate, they are prevented from connecting to the session\. Client authentication requirements can be disabled to allow clients to connect to a session without authenticating against the server\.

NICE DCV supports the following authentication methods:
+ `system` — This is the default authentication method\. Client authentication is delegated to the underlying operating system\. For Windows NICE DCV servers, authentication is delegated to WinLogon\. For Linux NICE DCV servers, authentication is delegated to PAM\. Clients provide their system credentials when connecting to a NICE DCV session\. Ensure that your clients have the credentials for the appropriate user accounts on the NICE DCV server\.
+ `none` — No client authentication is required when connecting to a NICE DCV session\. The NICE DCV server automatically grants access to all clients attempting to connect to a session\.

Make sure that your clients are aware of the authentication method used by the NICE DCV server, and that they have the information required to connect to the session\.

## Configuring Authentication on Windows<a name="set-authentication-windows"></a>

To change the NICE DCV server's authentication method, you must configure the `authentication` parameter using the Windows Registry Editor\.

**To change the authentication method on Windows**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/security/** key and select the **authentication** parameter\.

   If there is no `authentication` parameter in the registry key, create one:

   1. In the left\-hand pane, open the context \(right\-click\) menu for the **authentication** key and choose **New**, **string value**\.

   1. For **Name**, type `authentication` and press **Enter**\.

1. Open the **authentication** parameter\. For **Value data**, enter either `system` or `none`\.

1. Choose **OK** and close the Windows Registry Editor\.

## Configuring Authentication on Linux<a name="set-authentication-linux"></a>

To change the NICE DCV server's authentication method, you must configure the `authentication` parameter in the `dcv.conf` file\.

**To change the authentication method on Linux**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `authentication` parameter in the `[security]` section, and replace the existing value with either `system` or `none`\.

   If there is no `authentication` parameter in the `[security]` section, add it manually using the following format:

   ```
   [security] 
   authentication=method
   ```

1. Save and close the file\.