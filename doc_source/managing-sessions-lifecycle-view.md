# Viewing NICE DCV Sessions<a name="managing-sessions-lifecycle-view"></a>

The administrator on a Windows NICE DCV server or the root user on a Linux NICE DCV server can view all active sessions running on the server\. NICE DCV users can only view sessions that they have created\.

**To view the active console or virtual sessions on a Windows or Linux NICE DCV server**  
Use the `dcv list-sessions` command:

```
dcv list-sessions
```

The command returns a list of active sessions in the following format:

```
Session: session_id (owner: session_owner)
```