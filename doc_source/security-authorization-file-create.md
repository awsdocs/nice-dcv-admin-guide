# Working with Permissions Files<a name="security-authorization-file-create"></a>

You can create a custom permissions file or update an existing permissions file using your preferred text editor\. A permissions file typically takes the following format:

```
#import file_to_import

[groups]
group_definitions
				
[aliases]
alias_definitions
				
[permissions]
user_permissions
```

The following sections explain how to populate the sections when updating or creating a permissions file\.

**Contents**
+ [Import a Permissions File](#security-authorization-file-create-import)
+ [Create Groups](#security-authorization-file-create-group)
+ [Create Aliases](#security-authorization-file-create-alias)
+ [Add Permissions](#security-authorization-file-create-permission)

## Import a Permissions File<a name="security-authorization-file-create-import"></a>

The `imports` section is typically the first section of the permissions file\. This section lets you reference and include existing permissions files\. This enables you to incorporate previously defined NICE DCV permissions into your permissions file\.

A permissions file can include multiple imports\. An imported permissions file might import other permissions files\.

**To import a permissions file into your permissions file**
+ Use the `#import` statement and specify the location of the file with an absolute or a relative path\.\.
  + Windows NICE DCV server:

    ```
    #import ..\file_path\file
    ```
  + Linux NICE DCV server:

    ```
    #import ../file_path/file
    ```

**Example**  
The following statement imports a permissions file named `dcv-permissions.file` that is located in the NICE DCV installation folder on a Windows NICE DCV server using an absolute path:

```
#import c:\Program Files\NICE\DCV\dcv-permissions.file
```

## Create Groups<a name="security-authorization-file-create-group"></a>

The `[groups]` section of the permissions file lets you define user groups for users that have similar use cases or permissions requirements\. Groups can be assigned specific permissions\. Permissions assigned to a group apply to all of the users that are included in the group\.

To create groups in your permissions file, you must first add the groups section heading to the file\.

```
[groups]
```

You can then create your groups under the section heading\. To create a group, provide the group name, and then specify the group members in a comma\-separated list\. Group members can be individual users, other groups, and operating system user groups\.

```
group_name=member_1, member_2, member_3
```

**To add a user to a group**  
Specify the user name\.

**Note**  
You can prefix the user name with `user:`\. Windows domain user names can include a domain name\.

```
group_name=user_1, user:user_2, domain_name\user_3
```

**To add an existing group to a group**  
Specify the group name prefixed with `group:`

```
group_name=group:group_1, group:group_2
```

**To add an operating system user group to a group \(Linux NICE DCV servers only\)**  
Specify the group's name prefixed with `osgroup:`

```
group_name=osgroup:os_group_1, osgroup:os_group2
```

**Example**  
The following example adds the groups section heading and creates a group named `my-group` that includes individual users named `john` and `jane`, an existing group named `observers`, and an operating system user group named `guests`:

```
[groups]
my-group=john, user:jane, group:observers, osgroup:guests
```

## Create Aliases<a name="security-authorization-file-create-alias"></a>

The `[aliases]` section of the permissions file lets you create sets of NICE DCV features\. After an alias has been defined, you can grant or deny groups or individual users permissions to use it\. Granting or denying permissions to an alias grants or denies permissions to all of the features that are included in it\.

To create aliases in your permissions file, you must first add the aliases section heading to the file\.

```
[aliases]
```

You can then create your aliases under the section heading\. To create an alias, provide the alias name, and then specify the alias members in a comma\-separated list\. Alias members can be individual NICE DCV features or other aliases\.

```
alias_name=member_1, member_2, member_3
```

**Example**  
The following example adds the aliases section heading and creates an alias named `file-management` that includes the `file-upload` and `file-download` features and an existing alias named `clipboard-management`\.

```
[aliases]
file-management=file-upload, file-download, clipboard-management
```

## Add Permissions<a name="security-authorization-file-create-permission"></a>

The `[permissions]` section of the permissions file lets you control user and group access to specific features or aliases\.

To add permissions to your permissions file, first add the permissions section heading to the file\.

```
[permissions]
```

You can then add your permissions under the section heading\. To add a permission, specify the actor that it governs, the rule to be applied, and the features that it applies to\.

```
actor rule features
```

The actor can be a user, a group, or an operating system group\. Groups must be prefixed with `group:`\. Operating system groups must be prefixed with `osgroup:`\. NICE DCV includes a built\-in `%owner%` reference that can be used to refer to the session owner and a built\-in `%any%` reference that can be used to refer to any user\.

The following rules can be used in permissions statements:
+ `allow` — Grants access to the feature\.
+ `disallow` — Denies access to the feature, but can be overridden by subsequent permissions\.
+ `deny` — Denies access to the feature and cannot be overridden by subsequent permissions\.

The features can include individual NICE DCV features, aliases, or a combination of both\. The list of features must be separated by a space\. NICE DCV includes a built\-in `builtin` alias that includes all of the NICE DCV features\.

The following features can be referenced in the permissions file:
+ `display` — Receive visual data from the NICE DCV server\.
+ `clipboard-copy` — Copy data from the NICE DCV server to the client clipboard\.
+ `clipboard-paste` — Paste data from the client clipboard to the NICE DCV server\.
+ `file-download` — Download files from the session storage\.
+ `file-upload` — Upload files to the session storage\.
+ `mouse` — Input from the client pointer to the NICE DCV server\.
+ `keyboard` — Input from the client keyboard to the NICE DCV server\.
+ `keyboard-sas` — Use the secure attention sequence \(**CTRL\+Alt\+Del**\)\. Requires the `keyboard` feature\. Supported on version DCV 2017\.3 and later\.
+ `touch` — Use native touch events\. Supported on version DCV 2017\.3 and later\. Not supported on Linux NICE DCV servers\.
+ `stylus` — Input from specialized USB devices, such as 3D pointing devices or graphic tablets\.
+ `usb` — Read the smart card from the client\.
+ `pointer` — View NICE DCV server mouse position events and pointer shapes\. Supported on version DCV 2017\.3 and later\.
+ `audio-out` — Play back NICE DCV server audio on the client\.
+ `audio-in` — Insert audio from the client to the NICE DCV server\.
+ `printer` — Print PDFs or XPS files from the NICE DCV server to the client\.
+ `smartcard` — Read the smart card from the client\.
+ `builtin` — All features\.

**Example**  
The following example adds the permissions section heading and adds four permissions\. The first permission grants a user named `john` access to the `display`, `file-upload`, and `file-download` features\. The second permission denies the `observers` group access to the `audio-in` and `audio-out` features, and the `clipboard-management` feature alias\. The third permission grants the `guests` operating system group access to the `clipboard-management` and `file-management` aliases\. The fourth permission grants the session owner access to all features\.

```
[permissions]
john allow display file-upload file-download			
group:observers deny audio-in audio-out clipboard-management
osgroup:guests allow clipboard-management file-management
%owner% allow builtin
```