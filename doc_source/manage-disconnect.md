# Disconnecting Idle Clients<a name="manage-disconnect"></a>

You can configure NICE DCV to disconnect idle clients that have not sent any keyboard or pointer input to the NICE DCV server for a specified period\. By default, the NICE DCV server disconnects NICE DCV clients that have been idle for a period of 60 minutes\.

You can also configure the NICE DCV server to send a notification to idle clients to inform them that their session is about to disconnect\. Timeout notifications are supported only with NICE DCV servers and clients version 2017\.4 and later\.

You can use the following procedures to specify a custom idle timeout period\.

**Topics**
+ [Changing the Idle Timeout Period on Windows](#manage-disconnect-windows)
+ [Changing the Idle Timeout Period on Linux](#manage-disconnect-linux)

## Changing the Idle Timeout Period on Windows<a name="manage-disconnect-windows"></a>

To change the NICE DCV server's idle timeout period, you must configure the `idle-timeout` parameter using the Windows Registry Editor\.

**To change the idle timeout period on Windows**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key and select the **idle\-timeout** parameter\.

   If the parameter does not exist, use the following steps to create it:

   1. In the left pane, open the context \(right\-click\) menu for the **connectivity** key, and choose **New**, **DWORD \(32\-bit\) value**\.

   1. For **Name**, enter `idle-timeout` and press **Enter**\.

1. Open the **idle\-timeout** parameter\. For **Value data**, enter a value for the idle timeout period \(in minutes\)\. To avoid disconnecting idle clients, enter `0`\.

1. Choose **OK** and close the Windows Registry Editor\.

**\(Optional\) To configure the NICE DCV server to send timeout notifications to idle clients**

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key and select the **idle\-timeout\-warning** parameter\.

   If the parameter does not exist, use the following steps to create it:

   1. In the left pane, open the context \(right\-click\) menu for the **connectivity** key and choose **New**, **DWORD \(32\-bit\) value**\.

   1. For **Name**, enter `idle-timeout-warning` and press **Enter**\.

1. Open the **idle\-timeout\-warning** parameter\. For **Value data**, enter \(in seconds\) the amount of time before idle timeout disconnection that the notification should be sent\. For example, if you want the notification to be sent two minutes before the idle timeout is reached, enter `120`\.

1. Choose **OK** and close the Windows Registry Editor\.

## Changing the Idle Timeout Period on Linux<a name="manage-disconnect-linux"></a>

To change the NICE DCV server's idle timeout period, you must configure the `idle-timeout` parameter in the `dcv.conf` file\.

**To change the idle timeout period on Linux**

1. Open `/etc/dcv/dcv.conf` with your preferred text editor\.

1. Locate the `idle-timeout` parameter in the `[connectivity]` section and replace the existing timeout period with the new timeout period \(in minutes\)\.

   If there is no `idle-timeout` parameter in the `[connectivity]` section, add it manually using the following format:

   ```
   [connectivity]
   idle-timeout=timeout_in_minutes
   ```

   To avoid disconnecting idle clients, enter `0`\.

1. \(Optional\) To configure the NICE DCV server to send timeout notifications to idle clients, add the `idle-timeout-warning` parameter to the `[connectivity]` section and specify \(in seconds\) the amount of time before idle timeout disconnection that the notification should be sent\.

   ```
   idle-timeout-warning=seconds_before_idle_timeout
   ```

   For example, if you want the notification to be sent two minutes before the idle timeout is reached, specify `120`\.

1. Save and close the file\.