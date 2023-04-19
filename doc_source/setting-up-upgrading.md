# Upgrading the NICE DCV Server<a name="setting-up-upgrading"></a>

The following topic describes how to upgrade the NICE DCV server\.

**Considerations**
+ NICE DCV server versions 2017 and later are compatible with NICE DCV client versions 2017 and later\. 
+ NICE DCV server license files are backward compatible with previous versions of the NICE DCV server\. For example,you can use a NICE DCV server version 2021 license with NICE DCV server version 2019\. 
+ NICE DCV server versions require at least the same version of the NICE DCV server license\. For example, if you use a NICE DCV server version 2021, you need a license version 2021 or later\. If you upgrade to a later NICE DCV server version, you must request compatible license files\. For more information, contact your NICE DCV distributor or reseller\. 

**Topics**
+ [Upgrading the NICE DCV Server on Windows](#upgrading-windows-upgrade)
+ [Upgrading the NICE DCV Server on Linux](#upgrading-linux)

## Upgrading the NICE DCV Server on Windows<a name="upgrading-windows-upgrade"></a>

**To upgrade the NICE DCV server on Windows**

1. Using an RDP client, connect to the NICE DCV server as the administrator\.

1. Ensure that there are no running NICE DCV sessions\. Use the `dcv list-sessions` NICE DCV command to check for any running sessions\. If there are running sessions, use the `dcv close-session` NICE DCV command to stop them\.

1. After you confirm that there are no running sessions, stop the NICE DCV server\. For more information, see [Stopping the NICE DCV Server on Windows](manage-stop.md#manage-stop-windows)\.

1. Back up your NICE DCV server configuration\. Open the Registry Editor, navigate to **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv**, right\-click the **dcv** key, and choose **Export**\.

1. Download the latest version of the NICE DCV Server from the [NICE](http://download.nice-dcv.com) website\.

1. Follow the steps described in [Using the wizard](setting-up-installing-wininstall.md#setting-up-installing-windows-wizard), starting at step 3\.

1. After the installation is complete, confirm that the NICE DCV server configuration is still correct\. Open the Registry Editor, navigate to **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv** and compare the parameters to the configuration that you exported in step 4\.

1. Test the NICE DCV server by starting a new NICE DCV session\. For more information, see [Starting NICE DCV sessions](managing-sessions-start.md)\.

## Upgrading the NICE DCV Server on Linux<a name="upgrading-linux"></a>

**To upgrade the NICE DCV server on Linux**

1. Use SSH to sign in to the server using the `root` user\.

1. Ensure that there are no running NICE DCV sessions\. Use the `dcv list-sessions` NICE DCV command to check for any running sessions\. If there are running sessions, use the `dcv close session` NICE DCV command to stop them\.

1. After you confirm that there are no running sessions, stop the NICE DCV server\. For more information, see [Stopping the NICE DCV Server on Linux](manage-stop.md#manage-stop-linux)\.

1. Back up your NICE DCV server configuration\. Copy the `/etc/dcv/dcv.conf` file to a safe location\.

1. Follow the steps described in [Install the NICE DCV Server](setting-up-installing-linux-server.md#linux-server-install)\.

1. After the installation is complete, confirm that the NICE DCV server configuration is still correct\. Open the file that you copied in step 4 and compare it to the `/etc/dcv/dcv.conf` file\.

1. Test the NICE DCV server by starting a new NICE DCV session\. For more information, see [Starting NICE DCV sessions](managing-sessions-start.md)\.
