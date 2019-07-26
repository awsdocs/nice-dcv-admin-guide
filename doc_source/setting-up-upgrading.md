# Upgrading the NICE DCV Server<a name="setting-up-upgrading"></a>

The following topic explains how to upgrade the NICE DCV server\.

**Note**  
If you are upgrading to a more current major version of the NICE DCV server, for example, from NICE DCV 2013 to NICE DCV 2017, ensure that your clients use the NICE DCV client with the matching major version number\.

**Topics**
+ [Upgrading the NICE DCV Server on Windows](#upgrading-windows-upgrade)
+ [Upgrade the NICE DCV Server on Linux](#upgrading-linux)

## Upgrading the NICE DCV Server on Windows<a name="upgrading-windows-upgrade"></a>

**To upgrade the NICE DCV server on Windows**

1. Using an RDP client, connect to the NICE DCV server as the administrator\.

1. Ensure that there are no running NICE DCV sessions\. Use the `dcv list-sessions` NICE DCV command to check for any running sessions\. If there are running sessions, use the `dcv close session` NICE DCV command to stop them\.

1. After you confirm that there are no running sessions, stop the NICE DCV Server\. For more information see [Stopping the NICE DCV Server on Windows](manage-stop.md#manage-stop-windows)\.

1. Back up your NICE DCV server configuration\. Open the Registry Editor, navigate to **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv**, right\-click the **dcv** key, and choose **Export**\.

1. If you are upgrading to NICE DCV 2017 from an older major version \(pre\-2017\), you must uninstall the current version before installing NICE DCV 2017\. You cannot run multiple versions of NICE DCV on the same server\.

   To uninstall the current version of NICE DCV, use the **Programs and Features** utility, which is in the Windows Control Panel\.

   After the uninstallation is complete, restart and reconnect to the NICE DCV server as the administrator, using an RDP client\.

1. Download the latest version of the NICE DCV Server from the [NICE](https://www.nice-software.com/download/nice-dcv-2017) website\.

1. Follow the steps described in [Using the Wizard](setting-up-installing-windows.md#setting-up-installing-windows-wizard), starting at **Step 3**\.

1. After the installation is complete, confirm that the NICE DCV server configuration is still correct\. Open the Registry Editor, navigate to **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv** and compare the parameters to the configuration that you exported in **Step 4**\.

1. Test the NICE DCV server by starting a new NICE DCV session\. For more information, see [Starting NICE DCV Sessions](managing-sessions-start.md)\.

## Upgrade the NICE DCV Server on Linux<a name="upgrading-linux"></a>

**To upgrade the NICE DCV server on Linux**

1. SSH into the server and log in by using the `root` user\.

1. Ensure that there are no running NICE DCV sessions\. Use the `dcv list-sessions` NICE DCV command to check for any running sessions\. If there are running sessions, use the `dcv close session` NICE DCV command to stop them\.

1. After you confirm that there are no running sessions, stop the NICE DCV Server\. For more information see [Stopping the NICE DCV Server on Linux](manage-stop.md#manage-stop-linux)\.

1. Back up your NICE DCV server configuration\. Copy the `/etc/dcv/dcv.conf` file to safe location\.

1. If you are upgrading to NICE DCV server 2017 from an older major version \(pre\-2017\), you must uninstall the current version before installing NICE DCV 2017\. You cannot run multiple versions of NICE DCV on the same server\.
   + If you are upgrading from NICE DCV 2012 or earlier, use the following command:

     ```
     $  rpm -e nice-dcv-server
     ```
   + If you are upgrading from NICE DCV 2013 or later, use the uninstaller located in `/opt/nice/dcv/bin/dcvuninstall`\.

   After the uninstallation is complete, restart the server, SSH back into it, and then log in as the `root` user\.

1. Follow the steps described in [Install the NICE DCV Server](setting-up-installing-linux-server.md#linux-server-install)\.

1. After the installation is complete, confirm that the NICE DCV server configuration is still correct\. Open the file that you copied in **Step 4**, and compare it to the `/etc/dcv/dcv.conf` file\.

1. Test the NICE DCV server by starting a new NICE DCV session\. For more information, see [Starting NICE DCV Sessions](managing-sessions-start.md)\.