# Find and Stop Idle Sessions<a name="stop-idle-sessions"></a>

You can identify idle NICE DCV sessions using the `dcv describe-sessions` CLI command with the `-j` command option\. Specifying the `-j` option configures the command to return the output in JSON format, which provides additional details about the session\.

For example, the following command returns information about a session named `my-session`\.

```
$ dcv describe-session my-session -j
```

Output:

```
{
    "id" : "my-session",
    "owner" : "dcvuser",
    "x11-display" : ":1",
    "x11-authority" : "/run/user/1009/dcv/test3.xauth",
    "num-of-connections" : 1,
    "creation-time" : "2019-05-13T13:21:19.262883Z",
    "last-disconnection-time" : "2019-05-14T12:32:14.357567Z",
    "licensing-mode" : "DEMO",
    "licenses" : [
        {
            "product" : "dcv",
            "status" : "LICENSED",
            "check-timestamp" : "2019-05-14T12:35:40Z",
            "expiration-date" : "2019-05-29T00:00:00Z"
        },
        {
            "product" : "dcv-gl",
            "status" : "LICENSED",
            "check-timestamp" : "2019-05-14T12:35:40Z",
            "expiration-date" : "2019-05-29T00:00:00Z"
        }
    ]
}
```

In the command output, the `num-of-connections` parameter indicates the number of active client connections\. A value of `0` indicates that there are no active client connections, and that the session is currently idle\. You can also use the `last-disconnection-time` parameter to determine when the session last had an active client connection\. 

You can create a script or cron job that uses this information to identify idle sessions\. Then you can stop using them by using the [`dcv stop-session`](managing-sessions-lifecycle-stop.md) command\.

**Note**  
Stopping a session closes all of the applications that are running in the session\.