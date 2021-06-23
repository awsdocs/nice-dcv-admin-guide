# Common Issues<a name="troubleshooting-issues"></a>

This topic lists some common issues\.

**Topics**
+ [Cursor Issues on a Windows NICE DCV Server](#troubleshooting-issues-cursor)
+ [Unable to connect server did not accept the websocket handshake error] (#troubleshooting-websocket)

## Cursor Issues on a Windows NICE DCV Server<a name="troubleshooting-issues-cursor"></a>

With NICE DCV servers running on Windows Server 2012 or Windows 8 and later, the mouse cursor always appears as an arrow\. This happens even when pausing on text entry fields or single\-click navigation items\. This could happen if there is no physical mouse attached to the server, or if there is no mouse device listed in Device Manager\.

**To resolve the issue**

1. Open Control Panel, and choose **Ease of Access Center**\.

1. Choose **Make the mouse easier to use**\.

1. Select **Turn on Mouse Keys**\. 

1. Choose **Apply**, **OK**\.

## Unable to connect server did not accept the websocket handshake error<a name="troubleshooting-websocket"></a>

Please check if you have correctly configured your firewall settings (and security group, if you are runnig DCV on EC2).
You can check by temporarly disabling the firewall. On RHEL7.x, you can use this command: **sudo systemctl stop firewalld**

