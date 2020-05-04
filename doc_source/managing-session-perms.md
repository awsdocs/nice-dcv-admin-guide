# Managing NICE DCV Session Authorization<a name="managing-session-perms"></a>

Authorization is used to grant or deny NICE DCV clients permissions to specific NICE DCV features\. Typically, authorization is configured when a NICE DCV session is started\. However, it is possible to edit the permissions for a running session\. For more information about NICE DCV authorization, see [Configuring NICE DCV Authorization](security-authorization.md)\.

**To modify the permissions for a running session**  
Use the `dcv set-permissions` command\. The following options can be used with the `dcv set-permissions` command\.

**\-\-session**  
Specifies the ID of the session for which to set the permissions\.

**\-\-reset\-builtin**  
Resets the session's permissions to the default session permissions\. The default permissions grants only the session owner full access to all features\.

**\-\-none**  
Revokes all permissions for the session\.

**\-\-file**  
Specifies the path to a custom permissions file\. If the specified file is empty, all permissions are revoked\. For more information about creating a custom permissions file, see [Working with Permissions Files](security-authorization-file-create.md)\.

## Examples<a name="session-perms-example"></a>

**Example 1—Revoking all permissions**  
The following example revokes all client permissions for a session with an ID of `my-session`\.

```
C:\> dcv set-permissions --session my-session --none
```

**Example 2—Specifying custom permissions**  
The following example specifies a custom permissions file named `perm-file.txt`, which is located in the `c:\dcv\` directory, for a session with an ID of `my-session`\.

```
C:\> dcv set-permissions --session my-session --file c:\dcv\perm-file.txt
```

**Example 3—Resetting the permissions**  
The following example resets the permissions to the defaults for a session with an ID of `my-session`\.

```
C:\> dcv set-permissions --session my-session --reset-builtin
```