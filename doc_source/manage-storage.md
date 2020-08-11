# Enabling Session Storage<a name="manage-storage"></a>

Session storage is a folder on the NICE DCV server that clients can access when they are connected to a specific NICE DCV session\. When you enable session storage for a session, clients can download files from, and upload files to, the specified folder\. This feature enables clients to share files while connected to a session\.

**Topics**
+ [Enabling Session Storage on Windows](#manage-storage-windows)
+ [Enabling Session Storage on Linux](#manage-storage-linux)

## Enabling Session Storage on a Windows NICE DCV Server<a name="manage-storage-windows"></a>

To enable session storage, first create the folder to use for session storage\. Then, configure the `storage-root` parameter using the Windows Registry Editor\.

**To enable session storage on Windows**

1. Create the folder to use for session storage \(for example, `c:\session-storage`\)\.

1. Configure the `storage-root` parameter\.

   1. Open the Windows Registry Editor\.

   1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/session\-management/automatic\-console\-session** key and select the **storage\-root** parameter\.

      If there is no `storage-root` parameter in the registry key, create one as follows:

      1. In the left pane, open the context \(right\-click\) menu for the **session\-management/automatic\-console\-session** key and choose **New**, **String**\.

      1. For **Name**, enter `storage-root` and press **Enter**\.

   1. Open the **storage\-root** parameter\. For **Value data**, enter the full path to the folder created in step 1\.

      You can also use `%home%` in the path to specify the home directory of the user who is currently signed in\. For example, the following path uses `c:\Users\username\storage\` as the session storage directory\.

      ```
      %home%/storage/
      ```
**Note**  
If the specified subdirectory does not exist, then session storage is disabled\.

   1. Choose **OK** and close the Windows Registry Editor\.

   1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

1. Start the session and specify the `--storage-root` option\. For more information, see [Starting NICE DCV Sessions](managing-sessions-start.md)\.

## Enabling Session Storage on a Linux NICE DCV Server<a name="manage-storage-linux"></a>

To enable session storage, you must create the folder to use for session storage and then configure the `storage-root` parameter in the `dcv.conf` file\.

**To enable session storage on Linux**

1. Create the folder to use for session storage \(for example, `/opt/session-storage/`\)\.

1. Configure the `storage-root` parameter\.

   1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

   1. Locate the `storage-root` parameter in the `[session-management/automatic-console-session]` section\. Replace the existing path with the full path to the folder that you created in step 1\.

      If there is no `storage-root` parameter in the `[session-management/automatic-console-session]` section, add it manually using the following format\.

      ```
      [session-management/automatic-console-session]
      storage-root="/opt/session-storage/"
      ```

      You can also use `%home%` in the path to specify the home directory of the user who is currently signed in\. For example, the following parameter uses the `$HOME/storage/` directory for session storage\.

      ```
      [session-management/automatic-console-session]
      storage-root="%home%/storage/"
      ```
**Note**  
If the specified subdirectory does not exist, then session storage is disabled\.

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

1. Start the session and specify the `--storage-root` option\. For more information, see [Starting NICE DCV Sessions](managing-sessions-start.md)\.