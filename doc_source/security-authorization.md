# Configuring NICE DCV Authorization<a name="security-authorization"></a>

Authorization is used to grant or deny NICE DCV clients permissions to specific NICE DCV features\. By default, the NICE DCV server grants the session owner full access to all features\. However, you can specify custom permissions for your users using a custom permissions file\.

## NICE DCV Features<a name="security-authorization-features"></a>

The following features can be referenced in the permissions file:
+ `display` — Receive visual data from the NICE DCV server\.
+ `clipboard-copy` — Copy data from the NICE DCV server to the client clipboard\.
+ `clipboard-paste` — Paste data from the client clipboard to the NICE DCV server\.
+ `file-download` — Download files from the session storage\.
+ `file-upload` — Upload files to the session storage\.
+ `mouse` — Input from the client pointer to the NICE DCV server\.
+ `keyboard` — Input from the client keyboard to the NICE DCV server\.
+ `keyboard-sas` — Use secure attention sequence \(Control \+ Alt \+ Del\)\. Requires the `keyboard` feature\. Supported on DCV 2017\.3 and later\.
+ `touch` — Use native touch events\. Supported on DCV 2017\.3 and later\. Not supported with Linux NICE DCV Servers\.
+ `pointer` — View NICE DCV server mouse position events and pointer shapes\. Supported on DCV 2017\.3 and later\.
+ `audio-out` — Play back NICE DCV server audio on the client\.
+ `audio-in` — Insert audio from the client to the NICE DCV server\.
+ `printer` — Print PDFs or XPS files from the NICE DCV server to the client\.
+ `smartcard` — Read the smart card from the client\.

## Permissions File<a name="security-authorization-file"></a>

The permissions file defines the NICE DCV features to which users have access when they connect to a session\. You can create a custom permissions file that defines what each user is allowed to do on a NICE DCV session\. If you do not specify a customer permissions file, the NICE DCV server applies the default user permissions\. Those permissions grant the session owner full access to all features, and deny access to all other users\. For more information, see [Creating a Permissions File](security-authorization-file-create.md)\.

After you have created your custom permissions file, you can reference it when starting a new session using the `--permissions-file` option with the `dcv create-session` command\. For more information about starting sessions, see [Starting NICE DCV Sessions](managing-sessions-start.md)\.