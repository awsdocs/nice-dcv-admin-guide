# NICE DCV Server Parameter Reference<a name="config-param-ref"></a>

The following table lists the parameters that can be configured to customize the NICE DCV server\.

**Note**  
The **Reload context** column in each table indicates when the parameter is reloaded\. Possible contexts include:  
`server`—The parameter is loaded once when the server is started\. If the parameter value is updated, the new value is loaded when the server is restarted\.
`session`—The parameter is loaded when the session is created\. If the parameter value is updated, the new value is loaded for subsequent sessions\.
`connection`—The parameter is loaded when a new client connection is established\. If the parameter value is updated, the new value is used for subsequent client connections\.
`custom`—The conditions under which the parameter loads is unique to this parameter\. See the parameter description for more information\.

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
+ [`audio` Parameters](#audio)
+ [`log` Parameters](#log)
+ [`windows` Parameters](#windows)
+ [`clipboard` Parameters](#clipboard)
+ [`smartcard` Parameters](#smartcard)
+ [Modifying Configuration Parameters](config-param-ref-modify.md)

## `connectivity` Parameters<a name="connectivity"></a>

 The following table describes the configuration parameters in the `[connectivity]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `connectivity` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| web\-port | DWORD \(32\-bit\) | server | 8443 | TCP port for the web client — Specifies the TCP port on which the DCV server listens for client connections\. The port number must be between 1024 and 65535\. | 
| web\-url\-path | String | server | '/' | URL path for the embedded web server — Specifies the URL path for the embedded web server, must start with '/'\. For example, setting it to /test/foo means that the web server is reachable at https://host:port/test/foo\. | 
| web\-root | String | server | '' | Document root for the embedded web server — Specifies the document root for the embedded web server\. | 
| web\-use\-hsts | DWORD \(32\-bit\) | server | true | Whether to use HSTS — Enables this to force browsers to prevent any communication being sent over HTTP\. All transfer to the webpage \(and all subdomains\) will be done using HTTPS instead\. | 
| ws\-keepalive\-interval | DWORD \(32\-bit\) | server | 10 | Websocket keepalive interval — Specifies the interval \(in seconds\) after which to send a keepalive message\. If set to 0, the keepalive message is disabled\. | 
| idle\-timeout | DWORD \(32\-bit\) | custom | 60 | Idle timeout — Specifies the number of minutes to wait before disconnecting idle clients\. Specify 0 to never disconnect idle clients\. This parameter value is read every 5 seconds\. | 
| idle\-timeout\-warning | DWORD \(32\-bit\) | custom | 350 | Idle timeout warning — Specifies the number of seconds relative to idle\-timeout to wait before warning idle clients about idle timeout disconnection\. Specify 0 to never warn idle clients\. | 

## `session-management` Parameters<a name="session_management"></a>

 The following table describes the configuration parameters in the `[session-management]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `session-management` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| max\-concurrent\-sessions | DWORD \(32\-bit\) | server | 0 | Maximum number of concurrent sessions — Specifies the maximum number of allowed concurrent sessions\. This limit currently applies only to virtual sessions, because console sessions are intrinsically limited to one\. Specify 0 to not enforce any limit\.  | 
| create\-session | DWORD \(32\-bit\) | server | false | Create a console session at server startup — Specifies whether to automatically create a console session \(with ID "console"\) at server startup\. | 
| max\-concurrent\-clients | DWORD \(32\-bit\) | session | \-1 | Maximum number of concurrent clients per session — Specifies the maximum number of concurrent clients per session\. If set to \-1, no limit is enforced\. To set the limit only for the automatic session, use 'max\-concurrent\-clients' of section 'session\-management/automatic\-console\-session'\. | 
| enable\-gl\-in\-virtual\-sessions | String | session | 'default\-on' | Whether to employ dcv\-gl feature — Specifies whether to use the dcv\-gl feature \(a license is required\)\. Allowed values: 'always\-on', 'always\-off', 'default\-on', 'default\-off'\. | 
| virtual\-session\-font\-path | String | session | '' | Whether to add special font paths — Specifies the path of special fonts\. Some applications require a special font to be passed to the X server\. | 
| virtual\-session\-default\-layout | String | session | \[\] | Default layout for virtual sessions — If this is set, Xdcv is configured to create the specified layout at startup\. Each monitor can be configured with resolution \(w,h\) and position \(x,y\)\. All specified monitors are enabled\. Default layout example value: \[\{'w':<800>, 'h':<600>, 'x':<0>, 'y': <0>\}, \{'w':<1024>, 'h':<768>, 'x':<800>, 'y':<0>\}\] For this setting, the maximum number of monitors \(specified in the virtual\-session\-monitors setting\) has more priority than the number of elements in the array\. For example, if five monitors have been set, but the maximum number of monitors is four, only the first four monitors are created\. If this key is set, the number of enabled monitors \(specified in the virtual\-session\-monitors setting\) is ignored\.  | 
| virtual\-session\-xdcv\-args | String | session | '' | Additional arguments to pass to Xdcv — Specifies any additional arguments to be passed to Xdcv\. | 

## `session-management/defaults` Parameters<a name="session_management_defaults"></a>

 The following table describes the configuration parameters in the `[session-management/defaults]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `session-management/defaults` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| permissions\-file | String | session | '' | Default permissions included in all sessions — Specifies the path to the permissions file to be automatically merged with the permissions selected by the user for each session\. If empty, use the 'default\.perm' file, which is located in /etc/dcv/ for Linux, or in the DCV installation folder \(for example, 'C:\\Program Files\\NICE\\DCV\\Server\\conf'\) for Windows\. | 

## `session-management/automatic-console-session` Parameters<a name="session_management_automatic_console_session"></a>

 The following table describes the configuration parameters in the `[session-management/automatic-console-session]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `session-management/automatic-console-session` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| max\-concurrent\-clients | DWORD \(32\-bit\) | server | \-1 | Maximum number of concurrent clients per session — Specifies the maximum number of concurrent clients allowed per session\. If set to \-1, no limit is enforced\. | 
| permissions\-file | String | server | '' | Permissions file for the automatic "console" session — Specifies the path to the permissions file to be used to check user access to DCV features\. If empty, only the owner has full access to the session\. | 
| owner | String | server | '' | Owner of the automatically created "console" session — Specifies the username of the "console" session owner\. If empty, the owner is the user who started the DCV server\. This setting is applied only to the "console" session automatically created at server startup when the create\-session setting is set to true\. | 
| storage\-root | String | server | '' | Path to file storage root folder — Specifies the full path to the folder to be used for console session storage\. If the storage\-root is empty or the folder does not exist, file storage is disabled\. | 

## `security` Parameters<a name="security"></a>

 The following table describes the configuration parameters in the `[security]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `security` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| authentication | String | server | 'system' | Authentication method — Specifies the client authentication method used by the DCV server\. Use 'system' to delegate client authentication to the underlying operating system\. Use 'none' to disable client authentication and grant access to all clients\. | 
| authentication\-threshold | DWORD \(32\-bit\) | server | 3 | Authentication threshold — Specifies how many times each client can fail authentication before the connection is closed by the server\. To allow unlimited authentication attempts, use 0\. | 
| passwd\-file | String | server | '' | Password file — Specifies the password file to be used to check user credentials \(only with dcv authentication mode\)\. If empty, use the default file in $\{XDG\_CONFIG\_HOME\}/NICE/dcv/passwd for Linux, or %CSIDL\_LOCAL\_APPDATA%\\NICE\\dcv\\passwd for Windows\. | 
| pam\-service\-name | String | server | 'dcv' | PAM service name — Specifies the name of the PAM configuration file used by DCV\. The default PAM service name is 'dcv' and corresponds with the /etc/pam\.d/dcv configuration file\. This parameter is only used if the 'system' authentication method is used\.  | 
| enable\-gssapi | DWORD \(32\-bit\) | server | false | Enable GSSAPI SASL mechanism — Enables or disables GSSAPI SASL mechanism, that allows DCV authentication with kerberos\. | 
| service\-name | String | server | 'dcv' | Service Name — The registered name of the service \(usually the protocol name\)\. | 
| server\-fqdn | String | server | '' | Server FQDN — Server fully qualified domain name\. Empty means gethostname\(\)\. | 
| user\-realm | String | server | '' | Server user realm — Specifies a user realm for the server\. | 
| ca\-file | String | server | '' | CA file — Specifies the file containing the certificate authorities \(CAs\) trusted by the DCV server\. If empty, use the default trust store provided by the system\. | 
| auth\-token\-verifier | String | server | '' | The endpoint of the authentication token verifier — Specifies the endpoint \(URL\) of the authentication token verifier used by the DCV server\. If empty, the internal authentication token verifier is used\. | 
| no\-tls\-strict | DWORD \(32\-bit\) | server | false | Disable strict certificate validation — Enables or disables strict certificate validation when connecting to an external authentication token verifier\. Strict certificate validation must be disabled if the authentication token verifier uses a self\-signed certificate\. | 
| allowed\-http\-host\-regex | String | server | '^\.\+$' | Allowed host regular expression — Specifies a regular expression pattern representing the host names that this DCV server can serve\. If the Host header of an incoming HTTP request does not match this pattern, the request itself fails with a 403 Forbidden status code\. This is a security measure to prevent HTTP Host header attacks\. The pattern must be a valid Javascript\-like regular expression\. Letters in the pattern match both uppercase and lowercase letters\. Example: '^\(www\\\.\)?example\\\.com$'\] | 
| allowed\-ws\-origin\-regex | String | server | '^https://\.\+$' | Allowed origins — Specifies a regular expression pattern representing the origins that this DCV server accepts\. When establishing a WebSocket connection, the Origin header field in the client's handshake indicates the origin of the script establishing the connection\. If the Origin header of an incoming HTTP request does not match this pattern, the request itself fails with a 403 Forbidden status code\. This is a security measure to prevent cross\-site WebSocket hijacking \(CSWSH\) attacks\. The pattern must be a valid Javascript\-like regular expression\. Letters in the pattern match both uppercase and lowercase letters\. The Origin header has the form: <scheme> "://" <host> \[ ":" <port> \]\. Example: '^https://\(www\\\.\)?example\\\.com\(:443\)?$' | 
| max\-connections\-per\-user | DWORD \(32\-bit\) | server | 10 | Maximum number of user's connections — Specifies the maximum number of allowed concurrent connections per user\. Exceeding connections are rejected\. | 
| connection\-estab\-timeout | DWORD \(32\-bit\) | server | 5 | Connection establishment timeout — Specifies the amount of time \(in seconds\) allowed for the connection procedure to be completed before timing out\. If the procedure takes more, then the connection is closed\. If set to 0, the connection establishment does not time out\. | 
| connection\-setup\-timeout | DWORD \(32\-bit\) | server | 5 | Channel connection setup timeout — Specifies the amount of time \(in seconds\) allowed for the channel connection setup procedure to be completed before timing out\. If the procedure takes more, then the channel is closed\. If set to 0, the channel connection setup does not time out\. | 
| auth\-connection\-setup\-timeout | DWORD \(32\-bit\) | server | 120 | Authentication channel connection setup timeout — Specifies the amount of time \(in seconds\) allowed for the authentication channel connection setup procedure to be completed before timing out\. If the procedure takes more, then the channel is closed\. If set to 0, the authentication channel connection setup timeout is disabled\. | 
| ciphers | String | server | 'ECDHE\-RSA\-AES128\-GCM\-SHA256:ECDHE\-ECDSA\-AES128\-GCM\-SHA256:ECDHE\-RSA\-AES256\-GCM\-SHA384:ECDHE\-ECDSA\-AES256\-GCM\-SHA384:ECDHE\-RSA\-AES128\-SHA256:ECDHE\-RSA\-AES256\-SHA384' | Cipher list used on the TLS connections — Specifies the cipher list used on TLS connections\. The cipher list must be separated using the character ":" and must be supported by openssl and the clients\. | 
| os\-auto\-lock | DWORD \(32\-bit\) | custom | true | Whether to lock the OS session when last client connection ends — If enabled, the OS session is locked when the last client connection is closed\. This setting is read every time the session is going to be closed\.  | 

## `license` Parameters<a name="license"></a>

 The following table describes the configuration parameters in the `[license]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `license` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| license\-file | String | session | '' | License — Specifies a demo license file or RLM server port and hostname\. If you are using a floating license on an RLM server, use this parameter to specify the RLM server's port and hostname in the port@hostname format\. If you are using an extended demo license, and you have not placed the license\.lic file in the default location, use this parameter to specify the full path of license\.lic license file\. If the default file does not exist, a demo license is used\. This value is read from the configuration and updated every time a new session is created\.  | 

## `input` Parameters<a name="input"></a>

 The following table describes the configuration parameters in the `[input]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `input` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| enable\-relative\-mouse | DWORD \(32\-bit\) | session | true | Whether to allow relative mouse movements — Whether to allow relative mouse movements\. | 
| enable\-autorepeat | DWORD \(32\-bit\) | session | true | Whether to allow autorepeat on Linux — Specifies whether to allow autorepeat for a single key\. Excludes key combinations and key modifiers\. | 
| enable\-touch | DWORD \(32\-bit\) | session | true | Whether to allow touch input — Specifies whether touch is enabled\. | 
| enable\-stylus | DWORD \(32\-bit\) | session | true | Whether to allow stylus input — Specifies whether a stylus is enabled\. | 

## `display` Parameters<a name="display"></a>

 The following table describes the configuration parameters in the `[display]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `display` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| max\-compressor\-threads | DWORD \(32\-bit\) | session | 4 | Max compressor threads — Specifies the maximum number of compressor threads\. | 
| target\-fps | DWORD \(32\-bit\) | session | 25 | Target frames per second — Specifies the maximum allowed frames per second\. A value of 0 means no limit\. | 
| grabber\-target\-fps | DWORD \(32\-bit\) | session | 0 | Target frames per second of frame grabber — The upper limit to grab frames per second\. A value of 0 defaults to target\-fps\. Note that this setting will not be recognized by all frame capture backends\.  | 
| enable\-qu | DWORD \(32\-bit\) | session | true | Whether to send quality updates — Specifies whether to send quality updates\. | 
| enable\-client\-resize | DWORD \(32\-bit\) | session | true | Whether to allow clients to set the display layout — Specifies whether clients are allowed to set the display layout\. | 
| max\-layout\-area | DWORD \(32\-bit\) | custom | 0 | Max layout area in pixels — The maximum area in pixels of a display layout requestable by the client\. Layouts that are larger than this limit will be ignored\. This maximum is meant to provide an upper bound to the amount of display data that must be sent, without providing constraints on the display layout geometry\. If set to 0, no limit is applied to layout area\. The setting is reloaded at each client layout request\. | 
| max\-head\-resolution | String | custom | \(4096, 2160\) | Max head resolution — The maximum resolution of a display head requestable by the client\. A display head is equivalent to a host monitor\. The setting is reloaded at each client layout request\. When a bigger head resolution is requested by a client, the server adjusts the resolution to make sure that it matches the maximum width and height values set by this option\. | 
| web\-client\-max\-head\-resolution | String | custom | \(1920, 1080\) | Max head resolution for web client — The maximum resolution of a display head requestable by a web client\. A display head is equivalent to a host monitor\. The setting is reloaded at each client layout request\. This setting is ignored in case the web client is setting the max resolution explicitly\. The max\-head\-resolution limitations option is applied on top of the max width and height values set by this option\. In case the value is set to \(0, 0\), it is ignored\.  | 
| min\-head\-resolution | String | custom | \(640, 480\) | Min head resolution — The minimum resolution of a display head requestable by the client\. A display head is equivalent to a host monitor\. The setting is reloaded at each client layout request\. When a smaller resolution is requested by a client, the server adjusts the resolution to make sure that it matches the minimum width and height values set by this option\. | 
| max\-num\-heads | DWORD \(32\-bit\) | custom | 4 | Max number of heads — Specifies the maximum number of display heads requestable by the client\. A display head is equivalent to a host monitor\. The setting is reloaded at each client layout request\. When a greater number of heads is requested by a client, the server adjusts the number of heads so that the value does not exceed the value set by this option\.  | 
| console\-session\-default\-layout | String | session | \[\] | Default screen resolution and position for console sessions — Specifies the default screen resolution and position for console sessions\. If this is set, DCV sets the requested layout at startup\. Each monitor can be configured with resolution \(w,h\) and position \(x,y\)\. All specified monitors are enabled\. Default layout example value: \[\{'w':<800>, 'h':<600>, 'x':<0>, 'y': <0>\}, \{'w':<1024>, 'h':<768>, 'x':<800>,'y':<0>\}\]  | 
| use\-grabber\-dirty\-region | DWORD \(32\-bit\) | session | true | Whether to use dirty regions — Specifies whether to use dirty screen regions\. If enabled, the grabber tries to compute new frames out of the dirty regions from the screen\. | 
| cuda\-devices | String | connection | \[\] | CUDA devices used for stream encoding — Specifies the list of local CUDA devices which DCV uses to distribute encoding and CUDA workloads\. Each device is identified by a number that can be retrieved from the nvidia\-smi command\. For example, cuda\-devices=\['0', '2'\] indicates that DCV uses two GPUs, with IDs 0 and 2\. This setting is similar to the CUDA\_VISIBLE\_DEVICES environment variable, but it only applies to DCV\. If the option is not set, DCV uses an incremental session index starting from 0 to pick the next device to use\.  | 

## `display/linux` Parameters<a name="display_linux"></a>

 The following table describes the configuration parameters in the `[display/linux]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `display/linux` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| gl\-displays | String | session | \[':0\.0'\] | 3D accelerated X displays — Specifies the list of local 3D accelerated X displays and screens used by DCV for OpenGL rendering in virtual sessions\. If this value is missing, you can't run OpenGL applications in virtual sessions\. This setting is ignored for console sessions\.  | 
| h264\-encoder\-displays | String | connection | \[\] | H\.264 encoder X displays — Specifies the list of local X displays and screens that support accelerated H\.264 encoding\. If empty, DCV uses the same display selected for OpenGL rendering\. This setting is useful only in cases when some of the GPUs installed on the system do not provide acceleration for H\.264 encoding using one of the supported technologies\. | 

## `audio` Parameters<a name="audio"></a>

 The following table describes the configuration parameters in the `[audio]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `audio` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| source\-channels | DWORD \(32\-bit\) | session | 2 | Number of channels played on the source device\. — The number of channels that should be considered when grabbing audio from the source device\. A device provided by a driver can support many channels, for instance the DCV driver support 8 channels, but DCV needs to know how many are effectively used in order to mix correctly\. The setting must lower or equal than the number of channels supported by the device\. 0 \(use all channels\), 2 \(stereo\), 4 \(4\.0 quadriphonic\), 6 \(5\.1 surround\), 8 \(7\.1 surround\)\. Default value 2 \(stereo\) | 

## `log` Parameters<a name="log"></a>

 The following table describes the configuration parameters in the `[log]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `log` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| directory | String | server | '' | Log output directory — Specifies the destination to which logs are saved\. If not specified it defaults to "C:\\ProgramData\\NICE\\DCV\\log\\" on Windows and to "/var/log/dcv/" on Linux\.  | 
| level | String | custom | 'info' | Log level — Specifies the log file verbosity level\. The verbosity levels \(in order of the amount of detail they provide\) are: 'error', 'warning', 'info', and 'debug'\. The new value is effective as soon as it is changed on the configuration and propagated to the DCV agent processes\. With versions <= 2019\.1, the log level on the DCV agent processes is only set when they start\. | 
| rotate | DWORD \(32\-bit\) | server | 10 | Number of log file rotations — Specifies the number of times that log files are rotated before being removed\. If the value is 0, old versions are removed rather than rotated\. | 
| transfer\-audit | String | server | 'none' | Transfer direction to audit — Specifies which transfer direction to audit\. If this parameter is enabled, a new CSV file logs transfers between the server and clients\. The allowed values are: 'none', 'server\-to\-client', 'client\-to\-server', and 'all'\. If this value is missing or equal to 'none', transfer audits are disabled and no file is created\. | 

## `windows` Parameters<a name="windows"></a>

 The following table describes the configuration parameters in the `[windows]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `windows` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| disable\-display\-sleep | DWORD \(32\-bit\) | session | true | Prevent display from entering power\-saving mode — Specifies whether to prevent the display from entering power\-saving mode\. | 
| printer | String | session | 'DCV printer' | Printer to be set as default — Specifies the name of the virtual DCV printer\. Defaults to 'DCV printer'\. The name is used to change the default printer on the system\. If set to an empty string, DCV will not change the current default printer\. | 

## `clipboard` Parameters<a name="clipboard"></a>

 The following table describes the configuration parameters in the `[clipboard]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `clipboard` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| enabled | DWORD \(32\-bit\) | session | true | Whether the clipboard feature should be enabled\. — If clipboard feature is disabled, users will not be able to use the clipboard remotization\. Clipboard monitoring will be disabled too\. | 
| max\-payload\-size | DWORD \(32\-bit\) | session | 20971520 | Maximum size of clipboard's data — Specifies the maximum size \(in bytes\) of clipboard data that can be transferred from server to clients\. If this value is missing, the default limit of 20 MB is enforced\. | 
| max\-text\-len | DWORD \(32\-bit\) | session | \-1 | Maximum number of characters of clipboard's text — Specifies the maximum number of characters of clipboard text that can be transferred from server to clients\. If this value is missing or set to \-1, no limit is enforced\. | 
| max\-image\-area | DWORD \(32\-bit\) | session | \-1 | Maximum area of clipboard's image — Specifies the maximum area \(number of pixels\) of clipboard images that can be transferred from server to clients\. If this value is missing or set to \-1, no limit is enforced\. | 
| primary\-selection\-paste | DWORD \(32\-bit\) | session | false | Enables the primary selection pasting on linux — Linux desktops support multiple clipboards: the clipboard and the primary selection\. The primary selection is updated or copied when content is selected\. It can then be pasted using the mouse's middle button or the Shift\+Insert key combination\. When enabled, the client's clipboard content will be also inserted in the primary selection\.  | 
| primary\-selection\-copy | DWORD \(32\-bit\) | session | false | Enables the primary selection copy from linux — Linux desktops supports multiple clipboards: the clipboard and the primary selection\. The primary selection is updated or copied when content is selected\. It can then be pasted using the mouse's middle button or with the Shift\+Insert key combination\. When enabled, the primary selection is monitored and updates are propagated to the client\.  | 
| update\-timeout | DWORD \(32\-bit\) | session | 200 | Update event notification timeout — Specifies the time in msec to wait from the last update event for sending the notification to the client\. Default value 200 msec\. | 

## `smartcard` Parameters<a name="smartcard"></a>

 The following table describes the configuration parameters in the `[smartcard]` section of the `/etc/dcv/dcv.conf` file for Linux NICE DCV servers, and the `smartcard` registry key for Windows NICE DCV servers\. 


| Parameter | Type \(Windows only\) | Reload context | Default value | Description | 
| --- | --- | --- | --- | --- | 
| enable\-cache | String | custom | 'default\-off' | Whether to enable smartcard caching messages\. — Enables or disables smart card caching\. When enabled, the NICE DCV server caches the last value received from the client's smart card\. Future calls are retrieved directly from the server's cache, instead of from client\. This helps to reduce the amount of traffic that is transferred between the client and the server, and improves performance\. Allowed values include 'always\-on', 'always\-off', 'default\-on', and 'default\-off'\. This value is read from the configuration every time a client smartcard application is started\.  | 