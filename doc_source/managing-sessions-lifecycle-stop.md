# Stopping NICE DCV Sessions<a name="managing-sessions-lifecycle-stop"></a>

A console session can only be stopped by the administrator on Windows NICE DCV servers, and the root user on Linux NICE DCV servers\. A virtual session on a Linux NICE DCV server can only be stopped by the root user or the NICE DCV user who created it\. 

**To stop a console or virtual session on a Windows or Linux NICE DCV servers**  
Use the `dcv close-session` command and specify the unique session ID:

```
dcv close-session session_id
```

For example, the following command stops a session with the unique ID of `my-session`:

```
dcv close-session my-session
```