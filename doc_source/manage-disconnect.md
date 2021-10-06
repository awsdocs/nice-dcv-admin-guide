# Disconnecting idle clients<a name="manage-disconnect"></a>

You can configure NICE DCV to disconnect idle clients\. More specifically, you can do this for clients that didn't send any keyboard or pointer input to the NICE DCV server for a specific period of time\. By default, the NICE DCV server disconnects NICE DCV clients after being idle for 60 minutes \(one hour\)\.

You can also configure the NICE DCV server to send a notification to idle clients\. The notification is to inform them that their session is about to disconnect\. Timeout notifications are supported only with NICE DCV servers and clients version 2017\.4 and later\.

You can use the following procedures to specify a custom idle timeout period\.

**Topics**
+ [Changing the idle timeout period on Windows](#manage-disconnect-windows)
+ [Changing the idle timeout period on Linux](#manage-disconnect-linux)

## Changing the idle timeout period on Windows<a name="manage-disconnect-windows"></a>

To change the NICE DCV server's idle timeout period, you must configure the `idle-timeout` parameter using the Windows Registry Editor\.

**To change the idle timeout period on Windows**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key and select the **idle\-timeout** parameter\.

   If the parameter can't be found, use the following steps to create it:

   1. In the navigation pane, open the context \(right\-click\) menu for the **connectivity** key\. Then, choose **New**, **DWORD \(32\-bit\) value**\.

   1. For **Name**, enter `idle-timeout` and press **Enter**\.

1. Open the **idle\-timeout** parameter\. For **Value data**, enter a value for the idle timeout period \(in minutes\)\. To avoid disconnecting idle clients, enter `0`\.

1. Choose **OK** and close the Windows Registry Editor\.

**\(Optional\) To configure the NICE DCV server to send timeout notifications to idle clients**

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key and select the **idle\-timeout\-warning** parameter\.

   If the parameter can't be found, use the following steps to create it:

   1. In the navigation pane, open the context \(right\-click\) menu for the **connectivity** key\. Then, choose **New**, **DWORD \(32\-bit\) value**\.

   1. For **Name**, enter `idle-timeout-warning` and press **Enter**\.

1. Open the **idle\-timeout\-warning** parameter\. For **Value data**, enter the number of seconds in advance of the disconnection that the associated warning notification is sent\. For example, if you want the notification to be sent two minutes before the idle timeout is reached, enter `120`\.

1. Choose **OK** and close the Windows Registry Editor\.

## Changing the idle timeout period on Linux<a name="manage-disconnect-linux"></a>

To change the NICE DCV server's idle timeout period, you must configure the `idle-timeout` parameter in the `dcv.conf` file\.

**To change the idle timeout period on Linux**

1. Open `/etc/dcv/dcv.conf` with your preferred text editor\.

1. Locate the `idle-timeout` parameter in the `[connectivity]` section\. Then, replace the existing timeout period with the new timeout period \(in minutes\)\.

   If there's no `idle-timeout` parameter in the `[connectivity]` section, add it manually using the following format:

   ```
   [connectivity]
   idle-timeout=timeout_in_minutes
   ```

   To avoid disconnecting idle clients, enter `0`\.

1. \(Optional\) To configure the NICE DCV server to send timeout notifications to idle clients, add the `idle-timeout-warning` parameter to the `[connectivity]` section and specify the number of seconds in advance of the disconnection that the associated warning notification is sent\.

   ```
   idle-timeout-warning=seconds_before_idle_timeout
   ```

   For example, if you want the notification to be sent two minutes before the idle timeout is reached, specify `120`\.

1. Save and close the file\.