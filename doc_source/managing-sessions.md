# Managing NICE DCV Sessions<a name="managing-sessions"></a>

You must create a NICE DCV session on your NICE DCV server that your clients can connect to\. Clients can only connect to a NICE DCV server if there is an active session\.

**Topics**
+ [Introduction to NICE DCV Sessions](#managing-sessions-intro)
+ [Using the Command Line Tool to Manage NICE DCV Sessions](managing-sessions-cli.md)
+ [Starting NICE DCV Sessions](managing-sessions-start.md)
+ [Stopping NICE DCV Sessions](managing-sessions-lifecycle-stop.md)
+ [Managing Running NICE DCV Sessions](managing-running-session.md)
+ [Viewing NICE DCV Sessions](managing-sessions-lifecycle-view.md)

## Introduction to NICE DCV Sessions<a name="managing-sessions-intro"></a>

Every NICE DCV session has the following attributes:
+ **ID** — Used to uniquely identify the session on the NICE DCV server\.
+ **Owner** — The NICE DCV user who created the session\. By default, only the owner can connect to the session\.

NICE DCV clients need this information to connect to the session\.

NICE DCV offers two types of sessions\.

### Console Sessions<a name="managing-sessions-intro-console"></a>

Console sessions are supported on Windows and Linux NICE DCV servers\. If you are using a Windows NICE DCV server, you are only able to use console sessions\.

Only one console session can be hosted on the NICE DCV server at a time\. Console sessions are created and managed by the Administrator on Windows NICE DCV servers and the root user on Linux NICE DCV servers\. 

With console sessions, NICE DCV captures the content of the X server\. NICE DCV console sessions have direct access to the NICE DCV server's GPU\. Only one X server session can run at a time, and therefore, only one NICE DCV console session can run at at time\.

**Note**  
You can't run console and virtual sessions on the same NICE DCV server at the same time\.

### Virtual Sessions<a name="managing-sessions-intro-virtual"></a>

Virtual sessions are supported on Linux NICE DCV servers only\.

You can host multiple virtual sessions on the same NICE DCV server simultaneously\. Virtual sessions are created and managed by NICE DCV users\. NICE DCV users can only manage sessions that they have created\. The root user can manage all virtual sessions that are currently running on the NICE DCV server\.

With virtual sessions, NICE DCV starts an X server instance and runs a desktop environment inside the X server\. NICE DCV starts a new dedicated X server instance for each virtual session\. Each virtual session uses the display provided by its X server instance\.

If the `dcv-gl` package is installed and licensed, NICE DCV virtual sessions share access to the server's GPUs\. To share hardware\-based OpenGL across multiple virtual sessions, you must connect the virtual X server instance to the GPU by configuring the `dcv-gl.conf` file\.

**Note**  
You can't run console and virtual sessions on the same NICE DCV server at the same time\.