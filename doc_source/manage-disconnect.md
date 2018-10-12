# Disconnecting Idle Clients<a name="manage-disconnect"></a>

NICE DCV can be configured to disconnect idle clients who have not sent any keyboard or pointer input to the NICE DCV server for a specified period\. By default, the NICE DCV server disconnects NICE DCV clients that have been idle for a period of 60 minutes\.

You can use the following procedures to specify a custom idle timeout period\.

## Changing the Idle Timeout Period on Windows<a name="manage-disconnect-windows"></a>

To change the NICE DCV server's idle timeout period, you must configure the `idle-timeout` parameter using the Windows Registry Editor\.

**To change the idle timeout period on Windows**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/connectivity/** key and select the **idle\-timeout** parameter\.

   If there is no `idle-timeout` parameter in the registry key, create one:

   1. In the left\-hand pane, open the context \(right\-click\) menu for the **connectivity** key and choose **New**, **DWORD \(32\-bit\) value**\.

   1. For **Name**, type `idle-timeout` and press **Enter**\.

1. Open the **idle\-timeout** parameter\. For **Value data**, enter a value for the idle timeout period \(in minutes\)\.
**Note**  
To avoid disconnecting idle clients, enter `0` for the `idle-timeout` parameter\.

1. Choose **OK** and close the Windows Registry Editor\.

## Changing the Idle Timeout Period on Linux<a name="manage-disconnect-linux"></a>

To change the NICE DCV server's idle timeout period, you must configure the `idle-timeout` parameter in the `dcv.conf` file\.

**To change the idle timeout period on Linux**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `idle-timeout` parameter in the `[connectivity]` section, and replace the existing timeout period with the new timeout period \(in minutes\)\.

   If there is no `idle-timeout` parameter in the `[connectivity]` section, add it manually using the following format:

   ```
   [connectivity]
   idle-timeout=timeout_in_minutes
   ```
**Note**  
To avoid disconnecting idle clients, enter `0` for the `idle-timeout` parameter\.

1. Save and close the file\.