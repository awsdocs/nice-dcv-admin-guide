# Starting NICE DCV Sessions<a name="managing-sessions-start"></a>

By default, a console session is automatically created on Windows NICE DCV servers after installation\. The default console session is owned by `Administrator` and has a default session ID of `console`\. If you chose to prevent the automatic console session when you installed the NICE DCV server, you must create one manually\. You can enable or disable the automatic console session at any time after you install the NICE DCV server\.

**Note**  
Linux NICE DCV servers do not get a default console after installation\.

If you are using a floating license on an on\-premises or alternative cloud\-based server and you exceed the maximum number of concurrent sessions supported by your license, you might get a `no licenses` error\. If you get this error, stop an unused session to release the license and try again\.

The NICE DCV server must be running to start a session\. For more information, see [Starting the NICE DCV Server](manage-start.md)\.

**Topics**
+ [Manually Starting Console and Virtual Sessions](#managing-sessions-start-manual)
+ [Enabling Automatic Console Sessions](#managing-sessions-start-auto)

## Manually Starting Console and Virtual Sessions<a name="managing-sessions-start-manual"></a>

You can start a NICE DCV session at any time\. You can only run one console session at a time\. If you are using a Linux NICE DCV server, you can run multiple virtual sessions simultaneously\.

To create a console or virtual session on a Windows or Linux NICE DCV server, use the `dcv create-session` command\.

**Topics**
+ [Syntax](#syntax)
+ [Options](#options)
+ [Examples](#managing-sessions-start-manual)

### Syntax<a name="syntax"></a>

```
dcv create-session --type console|virtual --name session_name --user username --owner owner_name --permissions-file /path_to/permissions_file --storage-root /path_to/storage_directory --gl on|off --max-concurrent-clients number_of_clients --init /path_to/init_script session_name
```

### Options<a name="options"></a>

The following options can be used with the `dcv create-session` command:

**`--type`**  
This option is supported on Linux NICE DCV servers only\. It specifies the type of session to be created and can be either `console` or `virtual`\.  
Type: String  
Allowed values: `console` \| `virtual`  
Required: No

**`--name`**  
Specifies a name for the session\. Session names can be any string of up to 256 characters\. If the string exceeds 256 characters, the command fails\. Session names don't need to be unique across running sessions\.  
You can change a session's name at any time using the `dcv set-name` command\. For more information, see [Managing the Session Name](managing-session-name.md)\.  
Type: String  
Required: Yes

**`--user`**  
This option is supported with virtual sessions on Linux NICE DCV sessions only\. This value is the user to be used to create the session\. Only the root user can impersonate other users\.  
Type: String  
Required: No

**`--owner`**  
Specifies the session owner\. Defaults to the currently signed in user if omitted\.  
Type: String  
Required: No

**`-permissions-file`\-**  
Specifies a path to a custom permissions file\. Defaults to the server defaults if omitted\.  
Type: String  
Required: No

**`--storage-root`**  
Specifies the path to the folder used for session storage\.  
You can use `%home%` to specify the home directory of the user who is currently signed in\. For example, the following sets the directory for session storage as `c:\Users\username\storage\` for Windows servers or `$HOME/storage/` for Linux servers\.  

```
--storage-root %home%/storage/
```
If a specified subdirectory does not exist, session storage is disabled\.
Type: String  
Required: No

**`--gl`**  
This option is supported with virtual sessions on Linux NICE DCV sessions only\. It overrides the default `dcv-gl` state and can be either `on` or `off`\.  
Type: String  
Allowed values: `on` \| `off`  
Required: No

**\-\-max\-concurrent\-clients**  
Specifies the maximum number of NICE DCV clients that are allowed to connect to the session\. Defaults to unlimited connections if omitted\.  
Type: Integer  
Required: No

**\-\-init**  
This option is supported with virtual sessions on Linux NICE DCV servers only\. It specifies the path to a custom `init` script\. The script can be used to start a specific desktop environment and launch specific applications automatically when the session starts\. The script must be executable\. Defaults to a script that starts the default desktop environment if omitted\.  
Type: String  
Required: No

### Examples<a name="managing-sessions-start-manual"></a>

**Example 1 \- Console session**  
The following command creates a `console` session owned by `dcv-user` with a unique session ID of `my-session`, and a session name of `my graphics session`\. It also specifies a permissions file named `perm-file.txt`\.
+ Windows NICE DCV server

  ```
  C:\> dcv create-session --owner dcv-user --name "my graphics session" --permissions-file perm-file.txt my-session
  ```
+ Linux NICE DCV server

  ```
  $ sudo dcv create-session --type=console --owner dcv-user --name "my graphics session" --permissions-file perm-file.txt my-session
  ```

**Example 2 \- Virtual Session \(Linux NICE DCV servers only\)**  
The following command creates a `virtual` session using the `root` user to impersonate the intended session owner, `dcv-user`\. The session is owned by `dcv-user` even though it is created by the root user\.

```
$ sudo dcv create-session --owner dcv-user --user dcv-user my-session
```

**Example 3 \- Virtual Session \(Linux NICE DCV servers only\)**  
The following command creates a `virtual` session owned by the user who creates it:

```
$ dcv create-session my-session
```

## Enabling Automatic Console Sessions<a name="managing-sessions-start-auto"></a>

Enabling an automatic console session ensures that a console session is automatically created each time that the NICE DCV server starts\. The automatic console session is owned by the NICE DCV user specified by the `owner` configuration parameter\. Its session ID is always `console`\.

Other parameters affecting automatic console sessions are `max-concurrent-clients`, `permissions-file`, and `storage-root`\. For more information about these parameters, see [`session-management/automatic-console-session` Parameters](config-param-ref.md#session_management_automatic_console_session)\.

**Note**  
NICE DCV does not support automatic virtual sessions\.

------
#### [ Windows NICE DCV server ]

**To enable an automatic console session on a Windows NICE DCV server**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/session\-management** key\.

1. Create a `create-session` parameter:

   1. In the left pane, open the context \(right\-click\) menu for the **session\-management** key and choose **New**, **DWORD \(32\-bit\) Value**\.

   1. For **Name**, enter `create-session` and press **Enter**\.

   1. Open the **create\-session** parameter\. For **Value data**, enter `1`, and choose **OK**\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/session\-management/automatic\-console\-session** key\.

1. Create an `owner` parameter:

   1. In the left pane, open the context \(right\-click\) menu for the **automatic\-console\-session** key and choose **New**, **String Value**\.

   1. For **Name**, enter `owner` and press **Enter**\.

   1. Open the **owner** parameter\. For **Value data**, enter the session owner's name and choose **OK**\.

1. Choose **OK** and close the Windows Registry Editor\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------
#### [ Linux NICE DCV server ]

**To enable an automatic console session on a Linux NICE DCV server**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Add the `create-session` and `owner` parameters to the `[session-management/automatic-console-session]` section using the following format:

   ```
   [session-management]
   create-session = true
   
   [session-management/automatic-console-session]
   owner="session-owner"
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------