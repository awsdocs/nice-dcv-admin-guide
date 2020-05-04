# Managing NICE DCV Session Storage<a name="managing-session-storage"></a>

Session storage is a directory on the NICE DCV server that clients can access when they are connected to a NICE DCV session\.

If session storage has been enabled on the NICE DCV server, you can use the `dcv set-storage-root` command to specify the directory to be used for session storage\. For more information about enabling session storage on the NICE DCV server, see [Enabling Session Storage](manage-storage.md)\.

**To set the session storage path**  
Use the `dcv set-storage-root` command and specify the session ID and the path to the directory to use\.

```
dcv set-storage-root --session session_id path/to/directory
```

You can use `%home%` to specify the home directory of the user who is currently signed in\. For example, the `%home%/storage/` path resolves to `c:\Users\username\storage\` on Windows servers\. It resolves to `$HOME/storage/` on Linux servers\. 

## Example<a name="session-storage-example"></a>

**Windows NICE DCV Server Example**  
The following example sets to storage path to `c:\session-storage` for a session with a session ID of `my-session`\.

```
C:\> dcv set-storage-root --session my-session c:\session-storage
```

**Linux NICE DCV Server Example**  
The following example sets to storage path to a directory named `session-storage` in the current user's home directory, for a session with a session ID of `my-session`\.

```
$ dcv set-storage-root --session my-session %home%/session-storage/
```