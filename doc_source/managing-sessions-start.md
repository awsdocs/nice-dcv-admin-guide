# Starting NICE DCV Sessions<a name="managing-sessions-start"></a>

By default, a console session is automatically created on Windows NICE DCV servers after installation\. The default console session is owned by `Administrator`, and has a default session ID of `console`\. If you chose to prevent the automatic console session when installing the NICE DCV server, you need to create one manually\. You can also enable or disable the automatic console session at any time after installing the NICE DCV server\.

**Note**  
Linux NICE DCV servers do not get a default console after installation\.

If you are using a floating license on an on\-premises or alternative cloud\-based server and you exceed the maximum number of concurrent sessions supported by your license, you could get a `no licenses` error\. If you get this error, stop an unused session to release the license and try again\.

The NICE DCV server must be running to start a session\. For more information, see [Starting the NICE DCV Server](manage-start.md)\.

**Contents**
+ [Manually Starting Console and Virtual Sessions](#managing-sessions-start-manual)
  + [Examples](#managing-sessions-start-manual)
+ [Enabling Automatic Console Sessions](#managing-sessions-start-auto)

## Manually Starting Console and Virtual Sessions<a name="managing-sessions-start-manual"></a>

You can start a NICE DCV session at any time\. You can only run one console session at a time\. If you are using a Linux NICE DCV server, you can run multiple virtual sessions simultaneously\.

**To create a console or virtual session on a Windows or Linux NICE DCV server**  
Use the `dcv create-session` command and specify the session type and a unique session ID\.

The following options can be used with the `dcv create-session` command:

**\-\-type=console\|virtual**  
This option is supported on Linux NICE DCV servers only\. It specifies the type of session to be created, and can be either `console` or `virtual`\.

**\-\-user**  
This option is supported with virtual sessions on Linux NICE DCV sessions only\. This value is the user to be used to create the session\. Only the root user can impersonate other users\.

**\-\-owner**  
Specifies the session owner\. Defaults to the currently logged in user if omitted\.

**\-\-permissions\-file**  
Specifies a path to a custom permissions file\. Defaults to the server defaults if omitted\.

**\-\-storage\-root**  
Specifies the path to the folder used for session storage\.

**\-\-gl**  
This option is supported with virtual sessions on Linux NICE DCV sessions only\. It overrides the default `dcv-gl` state, and can be either `on` or `off`\.

**\-\-max\-concurrent\-clients**  
Specifies the maximum number of NICE DCV clients that are allowed to connect to the session\. Defaults to unlimited connections if omitted\.

**\-\-init**  
This option is supported with virtual sessions on Linux NICE DCV servers only\. It specifies the path to a custom `init` script\. The script can be used to start a specific desktop environment and launch specific applications automatically when the session starts\. The script must be executable\. Defaults to a script that starts the default desktop environment if omitted\.

### Examples<a name="managing-sessions-start-manual"></a>

**Example 1 \- Console session**  
The following command creates a `console` session owned by `dcv-user` with a unique session ID `my-session`:
+ Windows NICE DCV server

  ```
  C:\> dcv create-session --owner dcv-user my-session
  ```
+ Linux NICE DCV server

  ```
  $ sudo dcv create-session --type=console --owner dcv-user my-session
  ```

**Example 2 \- Virtual Session**  
The following command creates a `virtual` session using the `root` user to impersonate the intended session owner, `dcv-user`\. The session is owned by `dcv-user` even though it is created by the root user\.

```
$ sudo dcv create-session --owner dcv-user --user dcv-user my-session
```

**Example 3 \- Virtual Session**  
The following command creates a `virtual` session owned by the user who creates it:

```
$ dcv create-session my-session
```

## Enabling Automatic Console Sessions<a name="managing-sessions-start-auto"></a>

Enabling an automatic console session ensures that a console session is automatically created each time that the NICE DCV server starts\. The automatic console session is owned by the NICE DCV user specified by the `owner` configuration parameter, and its session ID is always `console`\.

Other parameters affecting automatic console sessions are `max-concurrent-clients`, `permissions-file`, and `storage-root`\. For more information about these parameters, see [`session-management/automatic-console-session` Parameters](config-param-ref.md#session_management_automatic_console_session)\.

**Note**  
NICE DCV does not support automatic virtual sessions\.

**To enable an automatic console session on a Windows NICE DCV server**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/session\-management** key\.

1. Create a `create-session` parameter:

   1. Open the context \(right\-click\) menu for the **session\-management** key in the left\-hand panel and choose **New**, **DWORD \(32\-bit\) Value**\.

   1. For **Name**, type `create-session` and press **Enter**\.

   1. Open the **create\-session** parameter\. For **Value data**, type `1`, and choose **OK**\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/session\-management/automatic\-console\-session** key\.

1. Create an `owner` parameter:

   1. Open the context \(right\-click\) menu for the **automatic\-console\-session** key in the left\-hand panel and choose **New**, **String Value**\.

   1. For **Name**, type `owner` and press **Enter**\.

   1. Open the **owner** parameter\. For **Value data**, type the session owner's name and choose **OK**\.

1. Choose **OK** and close the Windows Registry Editor\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

**To enable an automatic console session on a Linux NICE DCV server**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Add the `create-session` and `owner` parameters to the `[session-management/automatic-console-session]` section using the following format:

   ```
   [session-management]
   create-session = true
   
   [session-management/automatic-console-session]
   owner="session_owner"
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.