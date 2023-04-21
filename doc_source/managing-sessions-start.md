# Starting NICE DCV sessions<a name="managing-sessions-start"></a>

When you use the defaults to [install Windows NICE DCV server](setting-up-installing-wininstall.md), a [console session](managing-sessions.md#managing-sessions-intro-console) is automatically created and active after the server is installed\. The default console session is owned by `Administrator` and has a default session ID of `console`\. You can use this session or you can [close it](managing-sessions-lifecycle-stop.md) and create a new session\.

If you chose to opt out of the automatic console session creation when you installed the NICE DCV server, you must create one manually\. After you install the NICE DCV server, you can enable or disable the [automatic console session creation](#managing-sessions-start-auto) at any time\.

**Note**  
Linux NICE DCV servers don't get a default console session after installation\.

Assume that you use a floating license on an on\-premises or alternative cloud\-based server and exceed the maximum number of concurrent sessions that's supported by your license\. You might get a `no licenses` error\. If you get this error, stop an unused session to release the license and try again\.

The NICE DCV server must be running to start a session\. For more information, see [Starting the NICE DCV Server](manage-start.md)\.

**Topics**
+ [Manually starting console and virtual sessions](#managing-sessions-start-manual)
+ [Enabling Automatic Console Sessions](#managing-sessions-start-auto)

## Manually starting console and virtual sessions<a name="managing-sessions-start-manual"></a>

You can start a NICE DCV session at any time\. You can only run one console session at a time\. If you're using a Linux NICE DCV server, you can run multiple virtual sessions at the same time\.

It's good practice to run `dcv list-sessions` before creating a session, especially if you're using Windows NICE DCV server\.

To create a console or virtual session on a Windows or Linux NICE DCV server, use the `dcv create-session` command\.

**Topics**
+ [Syntax](#managing-sessions-start-manual-syntax)
+ [Options](#managing-sessions-start-manual-options)
+ [Examples](#managing-sessions-start-manual-examples)

### Syntax<a name="managing-sessions-start-manual-syntax"></a>

The minimal syntax of the command to start a session is:

```
dcv create-session session_ID
```

The full syntax with all the options is:

```
dcv create-session \
    --type console|virtual \
    --name session_name \
    --user username \
    --owner owner_name \
    --permissions-file /path_to/permissions_file \
    --storage-root /path_to/storage_directory \
    --gl on|off \
    --max-concurrent-clients number_of_clients \
    --init /path_to/init_script \
    session_ID
```

**Note**  
The `\` symbol represents the syntax to split a command in multiple lines\.

You can also use `dcv create-session --help` to display a quick reference to the syntax\.

### Options<a name="managing-sessions-start-manual-options"></a>

The following options can be used with the `dcv create-session` command:

**`--type`**  
This option is supported on Linux NICE DCV servers only\. It specifies the type of session to be created and can be either `console` or `virtual`\.  
Type: String  
Allowed values: `console` \| `virtual`  
Required: No

**`--name`**  
Specifies a name for the session\. Session names can be any string of up to 256 characters\. If the string exceeds 256 characters, the command fails\. Session names don't need to be unique across running sessions\.  
You can change a session's name at any time using the `dcv set-name` command\. For more information, see [Managing the session name](managing-session-name.md)\.  
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

**`--permissions-file`**  
Specifies a path to a custom permissions file\. Defaults to the server defaults if omitted\.  
Type: String  
Required: No

**`--storage-root`**  
Specifies the path to the folder used for session storage\.  
You can use `%home%` to specify the home directory of the user who is currently signed in\. For example, the following sets the directory for session storage as `c:\Users\username\storage\` for Windows servers or `$HOME/storage/` for Linux servers\.  

```
--storage-root %home%/storage/
```
If a specified subdirectory doesn't exist, session storage is disabled\.
Type: String  
Required: No

**`--gl`**  
This option is supported with virtual sessions on Linux NICE DCV sessions only\. It overrides the default `dcv-gl` state and can be either `on` or `off`\.  
Type: String  
Allowed values: `on` \| `off`  
Required: No

**`--max-concurrent-clients`**  
Specifies the maximum number of NICE DCV clients that are allowed to connect to the session\. Defaults to unlimited connections if omitted\.  
Type: Integer  
Required: No

**`--init`**  
This option is supported with virtual sessions on Linux NICE DCV servers only\. It specifies the path to a custom `init` script\. The script can be used to start a specific desktop environment and launch specific applications automatically when the session starts\. The script must be executable\. Defaults to a script that starts the default desktop environment if omitted\.  
Type: String  
Required: No

**`session ID`**  
Provides an ID for your session at the end of the command\.  
Type: String  
Required: Yes

### Examples<a name="managing-sessions-start-manual-examples"></a>

**Example 1 \- Console session**  
The following command creates a console session owned by `dcv-user` with a unique session ID of `my-session`, and a session name of `my graphics session`\. It also specifies a permissions file named `perm-file.txt`\.
+ Windows NICE DCV server

  ```
  C:\> dcv create-session^
      --owner dcv-user^
      --name "my graphics session"^
      --permissions-file perm-file.txt^
      my-session
  ```
+ Linux NICE DCV server

  ```
  $ sudo dcv create-session \
      --type=console \
      --owner dcv-user \
      --name "my graphics session" \
      --permissions-file perm-file.txt \
      my-session
  ```

**Example 2 \- Virtual Session \(Linux NICE DCV servers only\)**  
The following command creates a virtual session using the root user to impersonate the intended session owner, `dcv-user`\. The session is owned by `dcv-user` even though it is created by the root user

```
$ sudo dcv create-session \
    --owner dcv-user \
    --user dcv-user \
    my-session
```

**Example 3 \- Virtual Session \(Linux NICE DCV servers only\)**  
The following command creates a virtual session owned by the user who creates it:

```
$ dcv create-session my-session
```

## Enabling Automatic Console Sessions<a name="managing-sessions-start-auto"></a>

Enabling an automatic console session ensures that a console session is automatically created each time that the NICE DCV server starts\. The automatic console session is owned by the NICE DCV user specified by the `owner` configuration parameter\. Its session ID is always `console`\.

Other parameters affecting automatic console sessions are `max-concurrent-clients`, `permissions-file`, and `storage-root`\. For more information about these parameters, see [`session-management/automatic-console-session` Parameters](config-param-ref.md#session_management_automatic_console_session)\.

**Note**  
NICE DCV doesn't support automatic virtual sessions\.

------
#### [ Windows NICE DCV server ]

**To enable an automatic console session on a Windows NICE DCV server**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/session\-management** key\.

1. Create a `create-session` parameter:

   1. In the navigation pane, open the context \(right\-click\) menu for the **session\-management** key and choose **New**, **DWORD \(32\-bit\) Value**\.

   1. For **Name**, enter `create-session` and press **Enter**\.

   1. Open the **create\-session** parameter\. For **Value data**, enter `1`, and choose **OK**\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/session\-management/automatic\-console\-session** key\.

1. Create an `owner` parameter:

   1. In the navigation pane, open the context \(right\-click\) menu for the **automatic\-console\-session** key and choose **New**, **String Value**\.

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