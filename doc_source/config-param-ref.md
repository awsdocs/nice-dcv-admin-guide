# NICE DCV Server Parameter Reference<a name="config-param-ref"></a>

The following table lists the parameters that can be configured to customize the NICE DCV server\.

For Windows NICE DCV servers, the configuration parameters must be configured using the Windows Registry Editor\. The parameters can be found by navigating to the `HKEY_USERS/S-1-5-18/Software/GSettings/com/nicesoftware/dcv/` registry path and selecting the key specified in the section heading\. If the parameter is not located in the specified key, add it using the type specified in the **Type** column, and the parameter as the name\.

For Linux NICE DCV servers, the configuration parameters must be configured in the `/etc/dcv/dcv.conf` file using your preferred text editor\. The parameters can be found by locating the relevant section in the file\. If the parameter is not listed below the section heading, add it using the `parameter_name="value"` format\.

**Topics**
+ [`connectivity` Parameters](#connectivity)
+ [`session-management` Parameters](#session_management)
+ [`session-management/defaults` Parameters](#session_management_defaults)
+ [`session-management/automatic-console-session` Parameters](#session_management_automatic_console_session)
+ [`security` Parameters](#security)
+ [`license` Parameters](#license)
+ [`input` Parameters](#input)
+ [`display` Parameters](#display)
+ [`display/linux` Parameters](#display_linux)
+ [`log` Parameters](#log)
+ [`windows` Parameters](#windows)
+ [`clipboard` Parameters](#clipboard)
+ [`smartcard` Parameters](#smartcard)

## `connectivity` Parameters<a name="connectivity"></a>

 The following table describes the configuration parameters in the `[connectivity]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `connectivity` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| web\-port | DWORD \(32\-bit\) | 8443 | TCP port for the web client — Specifies the TCP port on which the DCV server listens for client connections\. The port number must be between 1024 and 65535\. | 
| web\-url\-path | String | '/' | URL path for the embedded web server — Specifies the URL path for the embedded web server, must start with '/'\. For example, setting it to /test/foo means that the web server is reachable at https://host:port/test/foo\. | 
| web\-root | String | '' | Document root for the embedded web server — Specifies the document root for the embedded web server\. | 
| ws\-keepalive\-interval | DWORD \(32\-bit\) | 10 | Websocket keepalive interval — Specifies the interval \(in seconds\) after which to send a keepalive message\. If set to 0, the keepalive message is disabled\. | 
| idle\-timeout | DWORD \(32\-bit\) | 60 | Idle timeout — Specifies the number of minutes to wait before disconnecting idle clients\. Specify 0 to never disconnect idle clients\. | 

## `session-management` Parameters<a name="session_management"></a>

 The following table describes the configuration parameters in the `[session-management]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `session-management` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| create\-session | DWORD \(32\-bit\) | false | Create a console session at server startup — Specifies whether to automatically create a console session \(with ID "console"\) at server startup\. | 
| max\-concurrent\-clients | DWORD \(32\-bit\) | \-1 | Maximum number of concurrent clients per session — Specifies the maximum number of concurrent clients per session\. If set to \-1, no limit is enforced\. To set the limit only for the automatic session, use 'max\-concurrent\-clients' of section 'session\-management/automatic\-console\-session'\. | 
| enable\-gl\-in\-virtual\-sessions | String | 'default\-on' | Whether to employ dcv\-gl feature — Specifies whether to use the dcv\-gl feature \(a license is required\)\. Allowed values: 'always\-on', 'always\-off', 'default\-on', 'default\-off'\. | 
| virtual\-session\-font\-path | String | '' | Whether to add special font paths — Specifies the path of special fonts\. Some applications require a special font to be passed to the X server\. | 
| virtual\-session\-xdcv\-args | String | '' | Additional arguments to pass to Xdcv — Specifies any additional arguments to be passed to Xdcv\. | 

## `session-management/defaults` Parameters<a name="session_management_defaults"></a>

 The following table describes the configuration parameters in the `[session-management/defaults]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `session-management/defaults` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| permissions\-file | String | '' | Default permissions included in all session — Specifies the path to the permissions file to be automatically merged with the permissions selected by the user for each session\. If empty, use the 'default\.perm' file, which is located in /etc/dcv/ for Linux, or in the DCV installation folder \(for example, 'C:\\Program Files\\NICE\\DCV\\Server\\conf'\) for Windows\. | 

## `session-management/automatic-console-session` Parameters<a name="session_management_automatic_console_session"></a>

 The following table describes the configuration parameters in the `[session-management/automatic-console-session]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `session-management/automatic-console-session` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| max\-concurrent\-clients | DWORD \(32\-bit\) | \-1 | Maximum number of concurrent clients per session — Specifies the maximum number of concurrent clients allowed per session\. If set to \-1, no limit is enforced\. | 
| permissions\-file | String | '' | Permissions file for the automatic "console" session — Specifies the path to the permissions file to be used to check user access to DCV features\. If empty, only the owner has full access to the session\. | 
| owner | String | '' | Owner of the automatically created "console" session — Specifies the user name of the "console" session owner\. If empty, the owner is the user who started the DCV server\. This setting is applied only to the "console" session automatically created at server startup when the create\-session setting is set to true\. | 
| storage\-root | String | '' | Path to file storage root folder — Specifies the full path to the folder to be used for console session storage\. If the storage\-root is empty or the folder does not exist, file storage is disabled\. | 

## `security` Parameters<a name="security"></a>

 The following table describes the configuration parameters in the `[security]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `security` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| authentication | String | 'system' | Authentication method — Specifies the client authentication method used by the DCV server\. Use 'system' to delegate client authentication to the underlying operating system\. Use 'none' to disable client authentication and grant access to all clients\. | 
| authentication\-threshold | DWORD \(32\-bit\) | 3 | Authentication threshold — Specifies how many times each client can fail authentication before the connection is closed by the server\. To allow unlimited authentication attempts, use 0\. | 
| passwd\-file | String | '' | Password file — Specifies the password file to be used to check user credentials \(only with dcv authentication mode\)\. If empty, use the default file in $\{XDG\_CONFIG\_HOME\}/NICE/dcv/passwd for Linux, or %CSIDL\_LOCAL\_APPDATA%\\NICE\\dcv\\passwd for Windows\. | 
| pam\-service\-name | String | 'dcv' | PAM service name — Specifies the name of the PAM configuration file used by DCV\. The default PAM service name is 'dcv' and corresponds with the /etc/pam\.d/dcv configuration file\. This parameter is only used if the 'system' authentication method is used\.  | 
| ca\-file | String | '' | CA file — Specifies the file containing the certificate authorities \(CAs\) trusted by the DCV server\. If empty, use the default trust store provided by the system\. | 
| auth\-token\-verifier | String | '' | The endpoint of the authentication token verifier — Specifies the endpoint \(URL\) of the authentication token verifier used by the DCV server\. If empty, the internal authentication token verifier is used\. | 
| no\-tls\-strict | DWORD \(32\-bit\) | false | Disable strict certificate validation — Enables or disables strict certificate validation when connecting to an external authentication token verifier\. Strict certificate validation must be disabled if the authentication token verifier uses a self\-signed certificate\. | 
| allowed\-http\-host\-regex | String | '^\.\+$' | Allowed host regular expression — Specifies a regular expression pattern representing the host names that this DCV server can serve\. If the Host header of an incoming HTTP request does not match this pattern, the request itself fails with a 403 Forbidden status code\. This is a security measure to prevent HTTP Host header attacks\. The pattern must be a valid Javascript\-like regular expression\. Letters in the pattern match both uppercase and lowercase letters\. Example: '^\(www\\\.\)?example\\\.com$'\] | 
| allowed\-ws\-origin\-regex | String | '^https://\.\+$' | Allowed origins — Specifies a regular expression pattern representing the origins that this DCV server accepts\. When establishing a WebSocket connection, the Origin header field in the client's handshake indicates the origin of the script establishing the connection\. If the Origin header of an incoming HTTP request does not match this pattern, the request itself fails with a 403 Forbidden status code\. This is a security measure to prevent cross\-site WebSocket hijacking \(CSWSH\) attacks\. The pattern must be a valid Javascript\-like regular expression\. Letters in the pattern match both uppercase and lowercase letters\. The Origin header has the form: <scheme> "://" <host> \[ ":" <port> \]\. Example: '^https://\(www\\\.\)?example\\\.com\(:443\)?$' | 
| max\-connections\-per\-user | DWORD \(32\-bit\) | 10 | Maximum number of user's connections — Specifies the maximum number of allowed concurrent connections per user\. Exceeding connections are rejected\. | 
| connection\-estab\-timeout | DWORD \(32\-bit\) | 5 | Connection establishment timeout — Specifies the amount of time \(in seconds\) allowed for the connection procedure to be completed before timing out\. If the procedure takes more, then the connection is closed\. If set to 0, the connection establishment does not time out\. | 
| connection\-setup\-timeout | DWORD \(32\-bit\) | 5 | Channel connection setup timeout — Specifies the amount of time \(in seconds\) allowed for the channel connection setup procedure to be completed before timing out\. If the procedure takes more, then the channel is closed\. If set to 0, the channel connection setup does not time out\. | 
| auth\-connection\-setup\-timeout | DWORD \(32\-bit\) | 120 | Authentication channel connection setup timeout — Specifies the amount of time \(in seconds\) allowed for the authentication channel connection setup procedure to be completed before timing out\. If the procedure takes more, then the channel is closed\. If set to 0, the authentication channel connection setup timeout is disabled\. | 
| ciphers | String | 'ECDHE\-RSA\-AES128\-GCM\-SHA256:ECDHE\-ECDSA\-AES128\-GCM\-SHA256:ECDHE\-RSA\-AES256\-GCM\-SHA384:ECDHE\-ECDSA\-AES256\-GCM\-SHA384:ECDHE\-RSA\-AES128\-SHA256:ECDHE\-RSA\-AES256\-SHA384' | Cipher list used on the TLS connections — Specifies the cipher list used on TLS connections\. The cipher list must be separated using the character ":" and must be supported by openssl and the clients\. | 
| os\-auto\-lock | DWORD \(32\-bit\) | true | Whether to lock the OS session when last client connection ends — If enabled, the OS session is locked when the last client connection is closed\.  | 

## `license` Parameters<a name="license"></a>

 The following table describes the configuration parameters in the `[license]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `license` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| license\-file | String | '' | License — Specifies a demo license file or RLM server port and hostname\. If you are using a floating license on an RLM server, use this parameter to specify the RLM server's port and hostname in the port@hostname format\. If you are using an extended demo license, and you have not placed the license\.lic file in the default location, use this parameter to specify the full path of license\.lic license file\. If the default file does not exist, a demo license is used\. This value is read from the configuration and updated every time a new session is created\.  | 

## `input` Parameters<a name="input"></a>

 The following table describes the configuration parameters in the `[input]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `input` registry key for Windows NICE DCV servers\.


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| enable\-autorepeat | DWORD \(32\-bit\) | true | Whether to allow autorepeat on Linux — Specifies whether to allow autorepeat for a single key\. Excludes key combinations and key modifiers\. | 

## `display` Parameters<a name="display"></a>

 The following table describes the configuration parameters in the `[display]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `display` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| max\-compressor\-threads | DWORD \(32\-bit\) | 4 | Max compressor threads — Specifies the maximum number of compressor threads\. | 
| target\-fps | DWORD \(32\-bit\) | 25 | Target frames per second — Specifies the maximum allowed frames per second\. A value of 0 means no limit\. | 
| enable\-qu | DWORD \(32\-bit\) | true | Whether to send quality updates — Specifies whether to send quality updates\. | 
| enable\-client\-resize | DWORD \(32\-bit\) | true | Whether to allow clients to set the display layout — Specifies whether clients are allowed to set the display layout\. | 
| max\-num\-heads | DWORD \(32\-bit\) | 4 | Max number of heads — Specifies the maximum number of heads\. | 
| console\-session\-default\-layout | String | \[\] | Default screen resolution and position for console sessions — Specifies the default screen resolution and position for console sessions\. If this is set, DCV sets the requested layout at startup\. Each monitor can be configured with resolution \(w,h\) and position \(x,y\)\. All specified monitors are enabled\. Default layout example value: \[\{'w':<800>, 'h':<600>, 'x':<0>, 'y': <0>\}, \{'w':<1024>, 'h':<768>, 'x':<800>,'y':<0>\}\]  | 
| use\-grabber\-dirty\-region | DWORD \(32\-bit\) | true | Whether to use dirty regions — Specifies whether to use dirty screen regions\. If enabled, the grabber tries to compute new frames out of the dirty regions from the screen\. | 
| cuda\-devices | String | \[\] | CUDA devices used for stream encoding — Specifies the list of local CUDA devices which DCV uses to distribute encoding and CUDA workloads\. Each device is identified by a number that can be retrieved from the nvidia\-smi command\. For example, cuda\-devices=\['0', '2'\] indicates that DCV uses two GPUs, with IDs 0 and 2\. This setting is similar to the CUDA\_VISIBLE\_DEVICES environment variable, but it only applies to DCV\.  | 

## `display/linux` Parameters<a name="display_linux"></a>

 The following table describes the configuration parameters in the `[display/linux]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `display/linux` registry key for Windows NICE DCV servers: \.


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| gl\-displays | String | \[':0\.0'\] | 3D accelerated X displays — Specifies the list of local 3D accelerated X displays and screens used by DCV for OpenGL rendering in virtual sessions\. If this value is missing, you can't run OpenGL applications in virtual sessions\. This setting is ignored for console and display sessions\. | 
| h264\-encoder\-displays | String | \[\] | H\.264 encoder X displays — Specifies the list of local X displays and screens that support accelerated H\.264 encoding\. If empty, DCV uses the same display selected for OpenGL rendering\. This setting is useful only in cases when some of the GPUs installed on the system do not provide acceleration for H\.264 encoding using one of the supported technologies\. | 

## `log` Parameters<a name="log"></a>

 The following table describes the configuration parameters in the `[log]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `log` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| directory | String | '' | Log output directory — Specifies the destination to which logs are saved\. | 
| level | String | 'info' | Log level — Specifies the log file verbosity level\. The verbosity levels \(in order of the amount of detail they provide\) are: error, warning, info, and debug\. | 
| rotate | DWORD \(32\-bit\) | 10 | Number of log file rotations — Specifies the number of times that log files are rotated before being removed\. If the value is 0, old versions are removed rather than rotated\. | 
| transfer\-audit | String | 'none' | Transfer direction to audit — Specifies which transfer direction to audit\. If this parameter is enabled, a new CSV file logs transfers between the server and clients\. The allowed values are: 'none', 'server\-to\-client', 'client\-to\-server', and 'all'\. If this value is missing or equal to 'none', transfer audits are disabled and no file is created\. | 

## `windows` Parameters<a name="windows"></a>

 The following table describes the configuration parameters in the `[windows]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `windows` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| disable\-display\-sleep | DWORD \(32\-bit\) | true | Prevent display from entering power\-saving mode — Specifies whether to prevent the display from entering power\-saving mode\. | 
| printer | String | 'DCV printer' | Printer to be set as default — Specifies the name of the virtual DCV printer\. Defaults to 'DCV printer'\. | 

## `clipboard` Parameters<a name="clipboard"></a>

 The following table describes the configuration parameters in the `[clipboard]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `clipboard` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| max\-payload\-size | DWORD \(32\-bit\) | 2097152 | Maximum size of clipboard's data — Specifies the maximum size \(in bytes\) of clipboard data that can be transferred from server to clients\. If this value is missing, the default limit of 2 MB is enforced\. | 
| max\-text\-len | DWORD \(32\-bit\) | \-1 | Maximum number of characters of clipboard's text — Specifies the maximum number of characters of clipboard text that can be transferred from server to clients\. If this value is missing or set to \-1, no limit is enforced\. | 
| max\-image\-area | DWORD \(32\-bit\) | \-1 | Maximum area of clipboard's image — Specifies the maximum area \(number of pixels\) of clipboard images that can be transferred from server to clients\. If this value is missing or set to \-1, no limit is enforced\. | 

## `smartcard` Parameters<a name="smartcard"></a>

 The following table describes the configuration parameters in the `[smartcard]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `smartcard` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Default value | Description | 
| --- | --- | --- | --- | 
| enable\-cache | String | 'default\-off' | Configures smart card caching — Enables or disables smart card caching\. When enabled, the NICE DCV server caches the last value received from the client's smart card\. Future calls are retrieved directly from the server's cache, instead of from client\. This helps to reduce the amount of traffic that is transferred between the client and the server, and improves performance\. Allowed values include 'always\-on', 'always\-off', 'default\-on', and 'default\-off'\.  | 