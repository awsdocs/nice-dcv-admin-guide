# Managing the Session Name<a name="managing-session-name"></a>

You can change the name of a running session at any time\. Session names enable you to quickly identify a specific session based on the name that you've assigned to it\. Session names don't need to be unique across running sessions\.

**To change the name of a running session**  
Use the `dcv set-name` command\. For `session`, specify the ID of the session for which to change the name, and for `name`, specify the name for the session\. The session name can be any string of up to 256 characters\. If the specified string exceeds 256 characters, the command fails\.

```
$ dcv set-name --session session-id --name "session-name"
```

**To remove the name from a running session**  
Use the `dcv set-name` command\. For `session`, specify the ID of the session from which to remove the name, and include the `--none` parameter\.

```
$ dcv set-name --session session-id --none
```

## Examples<a name="session-name-example"></a>

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