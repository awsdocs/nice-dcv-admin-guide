# Enable Remote X Connections to the X Server<a name="setup-xforwarding"></a>

By default, NICE DCV 2017 prevents the use of X forwarding, because of inherent security risks\. NICE DCV inherits this behavior from the newer versions of the Xorg server\. The NICE DCV server implements the following default inherited mitigations to minimize the security risks:
+ The NICE DCV server prevents X connections from the network\. The NICE DCV server is configured to start with `-nolisten tcp` command line option\. However, it is possible to change the default behavior to enable remote X connections to the X server\. For more information about this workaround, see [Enable Remote X Connections to the X Server](#enable-remotex)\.
+ The X server disables GLX indirect contexts\. Because of conflicts with DCV\-GL, there is currently no workaround to enable GLX indirect contexts\.

For more information about the security risks and the mitigations, see the [ X\.Org Security Advisory](https://www.x.org/wiki/Development/Security/Advisory-2014-12-09/)\.

## Enable Remote X Connections to the X Server<a name="enable-remotex"></a>

By default, NICE DCV is configured to start with the `-nolisten tcp` command line option to reduce exposure to the security risks\. However, it is possible to change the default behavior to enable X forwarding\.

**To enable X forwarding**  
Open `/etc/dcv/dcv.conf` using your preferred text editor\. Add the following to the end of the file:
+ To enable X forwarding over IPv4 and IPv6

  ```
  [session-management]
  virtual-session-xdcv-args="-listen tcp"
  ```
+ To enable X forwarding over IPv4 only

  ```
  [session-management]
  virtual-session-xdcv-args="-listen tcp -nolisten inet6"
  ```

**Note**  
Enabling X forwarding does not affect existing sessions, but only the new sessions started after it's enabled\. 

**To test the X forwarding**

1. Connect the NICE DCV session\.

1. Confirm that the NICE DCV server is listening on a port in the range between 6000\-6063\.

   ```
   $ netstat -punta | grep 600
   ```

1. Retrieve the NICE DCV session display number\.

   ```
   $ dcv describe-session session_name | grep display
   ```

1. SSH into the remote server on which the application is hosted\.

   ```
   $ ssh user@remote_server_ip
   ```

1. From the remote server, export the display environment variable to point to the X server of the NICE DCV session\.

   ```
   $ export DISPLAY=dcv_server_ip:display_number
   ```

1. From the remote server, run an application to test the X forwarding functionality\. For example:

   ```
   xterm
   ```

   The test application, in this case xterm, should appear in NICE DCV server's desktop environment\.