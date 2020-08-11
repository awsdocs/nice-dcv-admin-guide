# Using the Log Files<a name="troubleshooting-logs"></a>

The NICE DCV log files can be used to identify and troubleshoot problems with your NICE DCV server\. The NICE DCV log files can be found in the following location on your NICE DCV server:
+ Windows server

  ```
  C:\ProgramData\NICE\dcv\log\
  ```
**Note**  
The `ProgramData` folder might be hidden by default\. If you do not see the `ProgramData` folder, set your file browser to show hidden items\. Alternatively, enter `%programdata%` in the address bar and press **Enter**\.
+ Linux server

  ```
  /var/log/dcv/
  ```

The NICE DCV server enables you to configure the verbosity level of the log files\. The following verbosity levels are available:
+ `error` — Provides the least detail\. Includes errors only\.
+ `warning` — Includes errors and warnings\.
+ `info` — The default verbosity level\. Includes errors, warnings, and information messages\.
+ `debug` — Provides the most detail\. Provides detailed information that is useful for debugging issues\.

## Changing Log File Verbosity on Windows<a name="troubleshooting-logs-windows"></a>

To configure the log file verbosity, you must configure the `level` parameter using the Windows Registry Editor\.

**To change the log file verbosity on Windows**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/log/** key\.

1. Open the **level** parameter by double\-clicking\. For **Value data**, type either `error`, `warning`, `info`, or `debug`, depending on the required verbosity level\.

1. Choose **OK** and close the Windows Registry Editor\.

## Changing Log File Verbosity on Linux<a name="troubleshooting-logs-linux"></a>

To configure the log file verbosity, you must configure the `level` parameter in the `dcv.conf` file\.

**To change the log file verbosity on Linux**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `level` parameter in the `[log]` section, and replace the existing verbosity level with either `error`, `warning`, `info`, or `debug`\.

   ```
   [log]
   level="verbosity_level"
   ```

1. Save and close the file\.