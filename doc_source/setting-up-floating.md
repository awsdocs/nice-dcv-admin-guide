# Installing a Floating License<a name="setting-up-floating"></a>

When you purchase a floating license from NICE, you receive a `license.lic` file that defines the license\. To install the license, you must:

1. Modify the license file\.

1. Prepare the Reprise License Manager \(RLM\) server\.

1. Configure the NICE DCV server\.

**Contents**
+ [Step 1: Modify the License File](#setting-up-floating-modify)
+ [Step 2: Prepare the RLM Server](#setting-up-floating-prep)
+ [Step 3: Configure the NICE DCV Server](#setting-up-floating-config)

## Step 1: Modify the License File<a name="setting-up-floating-modify"></a>

The `license.lic` file that you receive from NICE specifies the following information:
+ The RLM server's hostname, `rlmhostid` identifier, and TCP port number
+ The NICE DCV products covered by the license, along with the following details for each product:
  + The major version covered by the license\. For example, `2017` for the 2017 NICE DCV products\.
  + The expiration date\. `Permanent` indicates that the license does not expire\.
  + The maximum number of concurrent sessions\. For example, `10` for 10 concurrent sessions on the server\.
  + The license checksum\.
  + The license signature\.

The following code block shows the format of the `license.lic` file:

```
HOST RLM_server_hostname RLM_server_identifier RLM_server_port
ISV nice ISV_port
LICENSE product_1 major_version expiration_date concurrent_sessions share=hi _ck=checksum sig="signature"
LICENSE product_2 major_version expiration_date concurrent_sessions share=hi _ck=checksum sig="signature"
```

The following code block shows an example of a `license.lic` file:

```
HOST My-RLM-server abcdef123456 5053
ISV nice
LICENSE nice dcv 2017 permanent 10 share=hi _ck=456789098a sig="abcdefghijklmnopqrstuvwxyz1234567890abcdefghijklmnopqrstuvwxyz1234567890ab"
LICENSE nice dcv-gl 2017 permanent 10 share=hi _ck=123454323x sig="1234567890abcdefghijklmnopqrstuvwxyz1234567890abcdefghijklmnopqrstuvwxyz12"
```

**To modify the `license.lic` file received from NICE**  
Open the file with your preferred text editor and add your RLM server's hostname and the TCP port number to the first line in the file, which starts with `HOST`\.

Specifying the the *ISV\_port* is optional\. This specifies the port on which the license server listens\. If you do not specify a port, a random port is used\. This could cause conflicts with your firewall configuration\.

**Note**  
Modifying any other part of the license corrupts the file's signature and invalidates the license\. The *RLM\_server\_identifier* corresponds to the `rlmhostid` identifier that was used to generate the license and cannot be modified\.

## Step 2: Prepare the RLM Server<a name="setting-up-floating-prep"></a>

The license file must be installed on an RLM server\. Any NICE DCV server that can access the RLM server can use the license\.

If you put the RLM server behind a firewall, be aware that the RLM license server listens on two separate TCP ports\. One is the main port, is specified in the license file `HOST` line and by default is `5053`\. The other is related to the ISV license, is specifed in the license file `ISV` line and if not specified is randomly assigned: if you want the server to use a fixed port \(e\.g\. for easier firewall configuration\) you need to define the ISV port in the license file\. See [Step 1: Modify the License File](#setting-up-floating-modify) for more details\. 

For more information about RLM, see the [Reprise Software](http://www.reprisesoftware.com/products/license-manager.php) website\.

**To prepare the RLM server on Windows**

1. On your RLM server, download the RLM License Administration Bundle from the [Reprise Software website](http://www.reprisesoftware.com/products/license-manager.php)\.

1. Extract the contents of the RLM License Administration Bundle to `C:\RLM`\.

1. Copy the `license.lic` file that you received from NICE to `C:\RLM\license\`\.

1. Copy the `nice.set` file from your NICE DCV server and place it in the `C:\RLM\` folder on your RLM server\.

   The `nice.set` file can be found in the following location on your NICE DCV server:
   + Windows NICE DCV server:

     ```
     C:\Program Files\NICE\DCV\Server\license\
     ```
   + Linux NICE DCV server:

     ```
     /usr/share/dcv/license/
     ```

1. On your RLM server, open a command prompt window and do the following:

   1. Create an `RLM` root folder:

      ```
      C:\> cd C:\RLM
      ```

   1. Install the RLM server as a Windows service\. For more information about the RLM startup options, see the [RLM License Administration Manual](http://www.reprisesoftware.com/RLM_Enduser.html)\.

      ```
      C:\> rlm.exe -nows -dlog C:\RLM\rlm.log -c C:\RLM\license -install_service -service_name dcv-rlm
      ```

1. Start the RLM server:

   ```
   C:\> net start dcv-rlm
   ```

1. Confirm that the RLM server is running and functioning as expected\.

   1. Open the `rlm.log` file located in `C:\RLM\` with your preferred text editor and confirm that the following line appears:
**Note**  
The contents of the `rlm.log` file might vary slightly depending on the RLM server version\.

      ```
      date_time (nice) Server started on license1 (hostid: host_id) for: dcv dcv-gl
      ```

   1. Run the following command:

      ```
      C:\RLM\rlmstat -a -c rlm_server_hostname@5053
      ```

**To prepare the RLM server on Linux**

1. Log into your RLM server as `root` and download the RLM License Administration Bundle from the [Reprise Software](http://www.reprisesoftware.com/products/license-manager.php) website\.

1. Create a user group and a new `rlm` user\.
**Note**  
This can be any valid user or service account\. We strongly recommend that this value not be the root account\.

   ```
   $ groupadd -r rlm
   ```

   ```
   $ useradd -r -g rlm -d "/opt/nice/rlm" -s /sbin/nologin -c "RLM License Server" rlm
   ```

1. Create the `/opt/nice/rlm` and `/opt/nice/rlm/license` folders needed for the RLM server:

   ```
   $ mkdir -p /opt/nice/rlm/license
   ```

1. Extract the contents of the RLM License Administration Bundle to `/opt/nice/rlm/`, and ensure that the files are owned by the `rlm` user:

   ```
   $ tar xvf x64_l1.admin.tar.gz -C /opt/nice/rlm/ –stripcomponents 1
   ```

   ```
   $ chown -R rlm:rlm /opt/nice/rlm
   ```

1. Copy the `license.lic` file that you received from NICE to `/opt/nice/rlm/license/`\.

1. Copy the `nice.set` file from your NICE DCV server and place it in `/opt/nice/rlm` on your RLM server\.

   The `nice.set` file can be found in the following location on your NICE DCV server:
   + Windows NICE DCV server:

     ```
     C:\Program Files\NICE\DCV\Server\license\
     ```
   + Linux NICE DCV server:

     ```
     /usr/share/dcv/license/
     ```

1. Start the RLM server:

   ```
   $ service dcv-rlm start
   ```

1. Verify that the RLM server is running and functioning as expected\. Open `var/log/rlm.log` with your preferred text editor and confirm that the following line appears:
**Note**  
The contents of the `rlm.log` might vary slightly depending on the RLM server version\.

   ```
   date_time (nice) Server started on license1 (hostid: host_id) for: dcv dcv-gl
   ```

1. Ensure that the RLM server starts automatically\.

   1. Create a file named `dcv-rlm` in the `/opt/nice/rlm/` folder:

      ```
      $ touch /opt/nice/rlm/dcv-rlm
      ```

   1. Open the file using your preferred text editor and add the following script\. Save and close the file\.

      ```
      #! /bin/sh
      # chkconfig: 35 99 01
      # description: The Reprise License Manager daemon.
      # processname: dcv-rlm
      
      ### BEGIN INIT INFO
      # Provides: dcv-rlm
      # Required-Start: $local_fs $remote_fs $syslog
      # Required-Stop: $local_fs $remote_fs $syslog
      # Default-Start: 3 4 5
      # Default-Stop: 0 1 2 6
      # Short-Description: The Reprise License Manager daemon.
      # Description: A service that runs the Reprise License Manager daemon.
      ### END INIT INFO
      
      # user used to run the daemon
      RLM_USER="rlm"
      
      # root of rlm installation
      RLM_ROOT="/opt/nice/rlm"
      
      # license directory (license files should have .lic extension)
      RLM_LICENSE_DIR="/opt/nice/rlm/license"
      
      # log file
      RLM_LOG_FILE="/var/log/rlm.log"
      
      _getpid() {
      	pidof -o $$ -o $PPID -o %PPID -x "$1"
      }
      
      start() {
      	echo -n "Starting rlm: "
      	touch ${RLM_LOG_FILE}
      	chown "${RLM_USER}" ${RLM_LOG_FILE}
      	su -p -s /bin/sh "${RLM_USER}" -c "${RLM_ROOT}/rlm -c ${RLM_LICENSE_DIR} \
      	    -nows -dlog +${RLM_LOG_FILE} &"
      	if [ $? -ne 0 ]; then
      		echo "FAILED"
      		return 1
      	fi
      	echo "OK"
      }
      
      stop() {
      	echo -n "Stopping rlm: "
      	pid=`_getpid ${RLM_ROOT}/rlm`
      	if [ -n "$pid" ]; then
      		kill $pid >/dev/null 2>&1
      		sleep 3
      		if [ -d "/proc/$pid" ] ; then
      			echo "FAILED"
      			return 1
      		fi
      	fi
      	echo "OK"
      }
      
      status() {
      	pid=`_getpid ${RLM_ROOT}/rlm`
      	if [ -z "$pid" ]; then
      		echo "rlm is stopped"
      		return 3
      	fi
      	echo "rlm (pid $pid) is running..."
      	return 0
      }
      
      restart() {
      	stop
      	start
      }
      
      case "$1" in
      	start)
      		start
      		;;
      	stop)
      		stop
      		;;
      	status)
      		status
      		;;
      	restart)
      		restart
      		;;
      	*)
      	echo $"Usage: $0 {start|stop|status|restart}"
      	exit 1
      esac
      
      exit $?
      
      # ex:ts=4:et:
      ```

   1. Make the script executable, copy it to `/etc/init.d/`, and then add it to the `chkconfig` utility:

      ```
      chmod +x /opt/nice/rlm/dcv-rlm 
      ```

      ```
      cp -a /opt/nice/rlm/dcv-rlm /etc/init.d/
      ```

      ```
      chkconfig --add dcv-rlm
      ```

## Step 3: Configure the NICE DCV Server<a name="setting-up-floating-config"></a>

Configure your NICE DCV server to use your RLM server\. To do this, you must configure the `license-file` configuration parameter on your NICE DCV server\.

**To configure the `license-file` configuration parameter on a Windows server**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/license/** key and select the **license\-file** parameter\.

   If there is no `license-file` parameter in the registry key, you must create one:

   1. Open the context \(right\-click\) menu for the **license** key in the left\-hand panel and choose **New**, **String Value**\.

   1. For **Name**, type `license-file` and press **Enter**\.

1. Open the **license\-file** parameter\. For **Value data**, type RLM server port and hostname in the `5053@RLM_server_hostname` format\.
**Note**  
You can use the RLM server IP address instead of its hostname\.

1. Choose **OK** and close the Windows Registry Editor\.

**To configure the `license-file` configuration parameter on a Linux server**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `license-file` parameter in the `[license]` section, and replace the existing path with the RLM server's port and hostname in the `5053@RLM_server_hostname` format\.

   If there is no `license-file` parameter in the `[license]` section, add it manually using the following format:

   ```
   license-file = "5053@RLM_server_hostname"
   ```
**Note**  
You can use the RLM server IP address instead of its hostname\.

1. Save and close the file\.