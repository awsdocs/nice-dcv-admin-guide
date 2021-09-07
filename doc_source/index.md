# NICE DCV Administrator Guide

-----
*****Copyright &copy; Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What Is NICE DCV?](what-is-dcv.md)
+ [NICE DCV Servers](servers.md)
+ [Setting up the NICE DCV server](setting-up.md)
   + [Installing the NICE DCV Server](setting-up-installing.md)
      + [Installing the NICE DCV Server on Windows](setting-up-installing-windows.md)
         + [Prerequisites for Windows NICE DCV server on Amazon EC2 instances](setting-up-installing-winprereq.md)
         + [Installing the NICE DCV Server on Windows](setting-up-installing-wininstall.md)
      + [Installing the NICE DCV Server on Linux](setting-up-installing-linux.md)
         + [Prerequisites for Linux NICE DCV servers](setting-up-installing-linux-prereq.md)
         + [Install the NICE DCV Server on Linux](setting-up-installing-linux-server.md)
         + [Post-Installation checks](setting-up-installing-linux-checks.md)
   + [Licensing the NICE DCV Server](setting-up-license.md)
      + [Installing an extended evaluation license](setting-up-evaluation.md)
      + [Installing a production license](setting-up-production.md)
   + [Upgrading the NICE DCV Server](setting-up-upgrading.md)
   + [Uninstalling the NICE DCV Server](setting-up-uninstalling.md)
+ [Managing the NICE DCV Server](manage.md)
   + [Starting the NICE DCV Server](manage-start.md)
   + [Stopping the NICE DCV Server](manage-stop.md)
   + [Changing the NICE DCV Server TCP port](manage-port.md)
   + [Disconnecting idle clients](manage-disconnect.md)
   + [Enabling GPU sharing on a Linux NICE DCV Server](manage-gpu.md)
   + [Changing the TLS certificate](manage-cert.md)
   + [Enabling USB remotization](manage-usb-remote.md)
   + [Configuring smart card caching](manage-smart-card.md)
   + [Enabling session storage](manage-storage.md)
   + [Configuring the printer on a Linux NICE DCV Server](manage-printer.md)
   + [Configuring the clipboard on a Linux NICE DCV Server](manage-clipboard.md)
   + [Enabling touchscreen and stylus support](enable-stylus.md)
   + [Configuring multi-channel audio](manage-audio.md)
   + [Enable the QUIC UDP transport protocol](enable-quic.md)
   + [Configuring HTTP headers](manage-headers.md)
   + [Configuring NICE DCV authentication](security-authentication.md)
   + [Configuring NICE DCV authorization](security-authorization.md)
      + [Working with permissions files](security-authorization-file-create.md)
+ [Managing NICE DCV Sessions](managing-sessions.md)
   + [Using the Command Line Tool to Manage NICE DCV Sessions](managing-sessions-cli.md)
   + [Starting NICE DCV Sessions](managing-sessions-start.md)
   + [Stopping NICE DCV Sessions](managing-sessions-lifecycle-stop.md)
   + [Managing Running NICE DCV Sessions](managing-running-session.md)
      + [Managing NICE DCV Session Storage](managing-session-storage.md)
      + [Managing NICE DCV Session Authorization](managing-session-perms.md)
      + [Managing the NICE DCV Session Display Layout](managing-session-display.md)
      + [Managing the Session Name](managing-session-name.md)
   + [Viewing NICE DCV Sessions](managing-sessions-lifecycle-view.md)
   + [Getting NICE DCV Session Screenshots](managing-sessions-lifecycle-screenshot.md)
   + [Set certificate validation policy](set-certificate-validation-policy.md)
+ [How to...](how-to.md)
   + [Use External Authentication](external-authentication.md)
   + [Find and Stop Idle Sessions](stop-idle-sessions.md)
   + [Enable Remote X Connections to the X Server](setup-xforwarding.md)
   + [Embed the NICE DCV web browser client inside an iFrame](embed-in-iframe.md)
+ [Troubleshooting NICE DCV](troubleshooting.md)
   + [Using the Log Files](troubleshooting-logs.md)
   + [Common Issues](troubleshooting-issues.md)
+ [NICE DCV Server Parameter Reference](config-param-ref.md)
   + [Modifying Configuration Parameters](config-param-ref-modify.md)
+ [NICE DCV end of support life](eosl.md)
+ [Release Notes and Document History for NICE DCV](doc-history-release-notes.md)