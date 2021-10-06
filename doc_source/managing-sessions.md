# Managing NICE DCV sessions<a name="managing-sessions"></a>

Before your clients can connect to one, you must create a NICE DCV session on your NICE DCV server\. Clients can only connect to a NICE DCV server if there's an active session\.

Every NICE DCV session has the following attributes:
+ **ID** — Used to identify a specific session on the NICE DCV server\.
+ **Owner** — The NICE DCV user who created the session\. By default, only an owner can connect to the session\.

NICE DCV clients need this information to connect to the session\.

**Topics**
+ [Introduction to NICE DCV sessions](#managing-sessions-intro)
+ [Using the command line tool to manage NICE DCV sessions](managing-sessions-cli.md)
+ [Starting NICE DCV sessions](managing-sessions-start.md)
+ [Stopping NICE DCV sessions](managing-sessions-lifecycle-stop.md)
+ [Managing running NICE DCV sessions](managing-running-session.md)
+ [Viewing NICE DCV sessions](managing-sessions-lifecycle-view.md)
+ [Getting NICE DCV Session screenshots](managing-sessions-lifecycle-screenshot.md)
+ [Set certificate validation policy](set-certificate-validation-policy.md)

## Introduction to NICE DCV sessions<a name="managing-sessions-intro"></a>

NICE DCV offers two types of sessions—console sessions and virtual sessions\. The following table summarizes the differences betweeen the two types of sessions\.


| Session type | Support | Multiple sessions | Required permissions | Direct screen capture | GPU\-accelerated OpenGL support | 
| --- | --- | --- | --- | --- | --- | 
| Console | Linux and Windows NICE DCV servers | No, only one console session allowed on each server | Only the admin user can start and close sessions | Yes | Yes, without additional software | 
| Virtual | Linux NICE DCV servers only | Yes, multiple virtual sessions are allowed on a single server | Any user can start and close sessions | No, a dedicated X server \(Xdcv\), runs for each virtual session\. The screen is captured from the X server\. | Yes, but requires the DCV\-GL package | 

### Console sessions<a name="managing-sessions-intro-console"></a>

Console sessions are supported on Windows and Linux NICE DCV servers\. If you're using a Windows NICE DCV server, you can only use console sessions\.

Only one console session can be hosted on the NICE DCV server at a time\. Console sessions are created and managed by the Administrator on Windows NICE DCV servers and the root user on Linux NICE DCV servers\. 

With console sessions, NICE DCV directly captures the content of the desktop screen\. If the server is configured with a GPU, NICE DCV console sessions have direct access to the GPU\.

**Note**  
You can't run console and virtual sessions on the same NICE DCV server at the same time\.

### Virtual Sessions<a name="managing-sessions-intro-virtual"></a>

Virtual sessions are supported on Linux NICE DCV servers only\.

You can host multiple virtual sessions on the same NICE DCV server at the same time\. Virtual sessions are created and managed by NICE DCV users\. NICE DCV users can only manage sessions that they have created\. The root user can manage all virtual sessions that are currently running on the NICE DCV server\.

With virtual sessions, NICE DCV starts an X server instance, `Xdcv`, and runs a desktop environment inside the X server\. NICE DCV starts a new dedicated X server instance for each virtual session\. Each virtual session uses the display provided by its X server instance\.

If the `dcv-gl` package is installed and licensed, NICE DCV virtual sessions share access to the server's GPUs\. To share hardware\-based OpenGL across multiple virtual sessions, you must connect the virtual X server instance to the GPU by configuring the `dcv-gl.conf` file\.

**Note**  
You can't run console and virtual sessions on the same NICE DCV server at the same time\.