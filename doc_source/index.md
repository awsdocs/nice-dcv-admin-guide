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
      + [Updating the production license](updating-licenses.md)
   + [Upgrading the NICE DCV Server](setting-up-upgrading.md)
   + [Uninstalling the NICE DCV Server](setting-up-uninstalling.md)
+ [Managing the NICE DCV Server](manage.md)
   + [Starting the NICE DCV Server](manage-start.md)
   + [Stopping the NICE DCV Server](manage-stop.md)
   + [Enabling the QUIC UDP transport protocol](enable-quic.md)
   + [Changing the NICE DCV Server TCP/UDP ports and listen address](manage-port-addr.md)
   + [Managing the TLS certificate](manage-cert.md)
   + [Disconnecting idle clients](manage-disconnect.md)
   + [Enabling GPU sharing on a Linux NICE DCV Server](manage-gpu.md)
   + [Enabling touchscreen and stylus support](enable-stylus.md)
   + [Enabling gamepad support](enable-gamepad.md)
   + [Enabling USB remotization](manage-usb-remote.md)
   + [Configuring smart card caching](manage-smart-card.md)
   + [Enabling session storage](manage-storage.md)
   + [Configuring the printer on a Linux NICE DCV Server](manage-printer.md)
   + [Configuring the clipboard on a Linux NICE DCV Server](manage-clipboard.md)
   + [Configuring multi-channel audio](manage-audio.md)
   + [Configuring HTTP headers](manage-headers.md)
   + [Configuring NICE DCV authentication](security-authentication.md)
   + [Configuring NICE DCV authorization](security-authorization.md)
      + [Working with permissions files](security-authorization-file-create.md)
+ [Managing NICE DCV sessions](managing-sessions.md)
   + [Using the command line tool to manage NICE DCV sessions](managing-sessions-cli.md)
   + [Starting NICE DCV sessions](managing-sessions-start.md)
   + [Stopping NICE DCV sessions](managing-sessions-lifecycle-stop.md)
   + [Managing running NICE DCV sessions](managing-running-session.md)
      + [Managing NICE DCV Session storage](managing-session-storage.md)
      + [Managing NICE DCV Session authorization](managing-session-perms.md)
      + [Managing the NICE DCV Session display layout](managing-session-display.md)
      + [Managing the session name](managing-session-name.md)
   + [Managing session time zone](managing-session-time-zone.md)
   + [Viewing NICE DCV sessions](managing-sessions-lifecycle-view.md)
   + [Getting NICE DCV Session screenshots](managing-sessions-lifecycle-screenshot.md)
+ [How to...](how-to.md)
   + [Use External Authentication](external-authentication.md)
   + [Find and Stop Idle Sessions](stop-idle-sessions.md)
   + [Enable Remote X Connections to the X Server](setup-xforwarding.md)
   + [Embed the NICE DCV web browser client inside an iFrame](embed-in-iframe.md)
+ [Troubleshooting NICE DCV](troubleshooting.md)
   + [Using the Log Files](troubleshooting-logs.md)
   + [Troubleshooting Virtual Session Creation on Linux](troubleshooting-linux-virtual-session-creation.md)
   + [Linux Sessions fail to start after UID change](linux-change-uid.md)
   + [Fixing Cursor Issues on Windows](fixing-windows-cursor-issues.md)
   + [Fixing Copy and Paste to IntelliJ IDEA](fixing-copy-paste-intellij.md)
   + [Redirection clarifications with self-signed certificates](redirection-clarifications-with-self-signed-certs.md)
+ [NICE DCV Server parameter reference](config-param-ref.md)
   + [Modifying Configuration Parameters](config-param-ref-modify.md)
+ [NICE DCV end of support life](eosl.md)
+ [Security](dcv-security.md)
   + [Data protection in NICE DCV](data-protection.md)
   + [Compliance validation for NICE DCV](security-compliance-validation.md)
+ [Release notes and document history for NICE DCV](doc-history-release-notes.md)