# Configuring the Printer on a Linux NICE DCV Server<a name="manage-printer"></a>

If you are using a supported Linux distribution, you must configure the NICE DCV server to support printing\. No additional configuration is required for Windows NICE DCV servers\.

**To enable printer redirection on your Linux NICE DCV server**

1. Install `cups` service on your server\.
   + Amazon Linux 2, RHEL, and CentOS

     ```
     $ sudo yum install cups
     ```
   + Ubuntu

     ```
     $ sudo apt-get install cups
     ```
   + SUSE Linux Enterprise

     ```
     $ sudo zypper install cups
     ```

1. Add the `dcv` user to the printer administrator group\. The name of the printer administrator group can vary by operating system\. For example, if your printer administrator group is named `lpadmin`, run the following command:

   ```
   $ usermod -a -G lpadmin dcv
   ```

1. Make sure that the printer administrator group is referenced in the `SystemGroup` parameter in the cups configuration file\. For example, if your printer administrator group is named `lpadmin`, use a text editor to open `/etc/cups/cups-file.conf` and look for the following line\.

   ```
   SystemGroup lpadmin
   ```

   If the line appears in the configuration file, the installation is complete\. Continue to the next step\.

   If the line does not appear in the configuration file, add it manually in the following format and then save and close the file\.

   ```
   SystemGroup printer_admin_groupname
   ```

1. \(SUSE Linux Enterprise only\) Make sure that the printer administrator group has permission to read the cups local certificate, which is located in the following directory: `/var/run/cups/certs/`\. For example, if your printer administrator group is named `lpadmin`, run the following command:

   ```
   $ sudo chgrp -R lpadmin /var/run/cups/certs/ && chmod g+x /var/run/cups/certs
   ```

1. Restart the `cups` service\.

   ```
   $ sudo systemctl restart cups
   ```

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

## Troubleshooting printer issues<a name="troubleshoot"></a>

SUSE Linux Enterprise and RHEL 8 might prevent connections to the printer socket\. If you are running one of these operating systems and you are having printing issues, you can check the log file to determine whether this is the cause\.

Using a text editor, open `/var/log/audit/audit.log` and check if you log has a line that is similar to the following:

```
type=AVC msg=audit(1617716179.487:504): avc:  denied  { connectto } for  pid=33933 comm="dcvcupsbackend" path=002F636F6D2F6E696365736F6674776172652F6463762F637570732F636F6E736F6C65 scontext=system_u:system_r:cupsd_t:s0-s0:c0.c1023 tcontext=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023 tclass=unix_stream_socket permissive=0
```

If a similar line appears in your log file, then the operating system is preventing access to the printer socket\.

To resolve the issue, you must create a cups policy that allows access to the printer socket\. To do this, perform the following steps:

1. Create the required policy file\. Using your preferred text editor, create a new file named `cupsd_policy` and add the following content\.

   ```
   #============= cupsd_t ==============
   allow cupsd_t unconfined_t:unix_stream_socket connectto;
   ```

1. Install the policy\.

   ```
   $ cat cupsd_policy | audit2allow -M cupsd_policy_module
   ```

   ```
   $ semodule -i cupsd_policy_module.pp
   ```