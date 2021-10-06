# Managing NICE DCV Session authorization<a name="managing-session-perms"></a>

Authorization is used to grant or deny NICE DCV clients permissions to specific NICE DCV features\. Typically, authorization is configured when a NICE DCV session is started\. However, it's possible to edit the permissions for a running session\. For more information about NICE DCV authorization, see [Configuring NICE DCV authorization](security-authorization.md)\.

To modify the permissions for a running session, use the `dcv set-permissions` command\.

**Topics**
+ [Syntax](#syntax)
+ [Options](#options)
+ [Examples](#session-perms-example)

## Syntax<a name="syntax"></a>

```
dcv set-permissions --session sessions_name --none | --reset-builtin | --file /path_to/permissions_file
```

You must specify either `--none`, `--reset-builtin`, or `--file`\.

## Options<a name="options"></a>

The following options can be used with the `dcv set-permissions` command\.

**\-\-session**  
Specifies the ID of the session to set the permissions for\.

**\-\-reset\-builtin**  
Resets the session's permissions to the default session permissions\. The default permissions grants only the session owner full access to all features\.

**\-\-none**  
Revokes all permissions for the session\.

**\-\-file**  
Specifies the path to a custom permissions file\. If the specified file is empty, all permissions are revoked\. For more information about creating a custom permissions file, see [Working with permissions files](security-authorization-file-create.md)\.

## Examples<a name="session-perms-example"></a>

**Example 1—Revoking all permissions**  
The following example revokes all client permissions for a session with an ID of `my-session`\.

```
C:\> dcv set-permissions --session my-session --none
```

**Example 2—Specifying custom permissions**  
The following example specifies a custom permissions file that's named `perm-file.txt` for a session with an ID of `my-session`\. This file is located in the `c:\dcv\` directory\. 

```
C:\> dcv set-permissions --session my-session --file c:\dcv\perm-file.txt
```

**Example 3—Resetting the permissions**  
The following example resets the permissions to the defaults for a session with an ID of `my-session`\.

```
C:\> dcv set-permissions --session my-session --reset-builtin
```