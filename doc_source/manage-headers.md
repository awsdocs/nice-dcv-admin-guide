# Configuring HTTP Headers<a name="manage-headers"></a>

You can configure the NICE DCV server to send additional HTTP response headers to the NICE DCV client when users connect to a session using the web browser client\. The response headers can provide additional information about the NICE DCV server that users are connecting to\.

**Topics**
+ [Configuring HTTP Headers on a Windows NICE DCV Server](#manage-headers-windows)
+ [Configuring HTTP Headers on a Linux NICE DCV Server](#manage-headers-linux)

## Configuring HTTP Headers on a Windows NICE DCV Server<a name="manage-headers-windows"></a>

To configure the HTTP headers on Windows, configure the `web-extra-http-headers` parameter using the Windows Registry Editor\.

**To configure the HTTP headers on Windows**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key\.

1. In the left pane, open the context \(right\-click\) menu for the **connectivity** key, and choose **New**, **String**\.

1. For **Name**, enter `web-extra-http-headers` and press **Enter**\.

1. Open the **web\-extra\-http\-headers** parameter\. For **Value data**, enter the HTTP header name and value in the following format:

   ```
   [("header-name", "header-value")]
   ```

   To specify multiple headers, add them in a comma\-separated list\. For example:

   ```
   [("header1-name", "header1-value"), ("header2-name", "header2-value")]
   ```

1. Choose **OK** and close the Windows Registry Editor\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

## Configuring HTTP Headers on a Linux NICE DCV Server<a name="manage-headers-linux"></a>

To configure the HTTP headers on Linux, configure the `web-extra-http-headers` parameter in the `dcv.conf` file\.

**To configure the HTTP headers on Linux**

1. Open `/etc/dcv/dcv.conf` with your preferred text editor\.

1. Locate the `[connectivity]` section\. Specify the HTTP header name and value in the following format: 

   ```
   [connectivity]
   web-extra-http-headers=[("header-name", "header-value")]
   ```

   To specify multiple headers, add them in a comma\-separated list\. For example:

   ```
   [connectivity]
   web-extra-http-headers=[("header1-name", "header1-value"), ("header2-name", "header2-value")]
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.