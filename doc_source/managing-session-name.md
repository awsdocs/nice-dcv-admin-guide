# Managing the session name<a name="managing-session-name"></a>

You can change the name of a running session at any time\. You can use the specific name of session to quickly identify a session based on its name\. Session names don't need to be unique across running sessions\.

To change the name of a running session, use the `dcv set-name` command\. 

**Topics**
+ [Syntax](#managing-session-name-syntax)
+ [Options](#managing-session-name-options)
+ [Examples](#example)

## Syntax<a name="managing-session-name-syntax"></a>

```
$ dcv set-name --session session_id --none |--name "session-name"
```

You must specify either `--name` or `--none`\.

## Options<a name="managing-session-name-options"></a>

The following options can be used with the `dset-name` command\.

**`--session`**  
The ID of the session to set the name for\.   
Type: String  
Required: Yes

**`--name`**  
The name to assign the session\. Only specify this option if you want to assign a name to session\. If you want to remove a name, omit this paramater\. The session name can be up to 256 characters long\. It can consist of letters, numbers, and special characters\. If the specified string exceeds 256 characters, the command fails\.  
Type: String  
Required: No

**`--none`**  
Specify this parameter to remove an existing name from a session\. If you don't want to remove the session name, omit this option\.  
Required: No

## Examples<a name="example"></a>

**Example 1—Changing a session's name**  
The following example sets the name of a session with an ID of `my-session` to `my graphics session`\.

```
$ dcv set-name --session my-session --name "my graphics sessions"
```

**Example 2—Removing a session's name**  
The following example removes the name of a session with an ID of `my-session`\.

```
$ dcv set-name --session my-session --none
```