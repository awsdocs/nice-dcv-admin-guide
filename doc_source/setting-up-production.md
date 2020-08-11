# Installing a Production License<a name="setting-up-production"></a>

The following sections in this topic explain how to purchase and use a production license \(perpetual license or subscription\)\.

**Topics**
+ [Step 1: Install the RLM Server](#install-rlm)
+ [Step 2: Get the RLM Server's Host ID](#hostid-rlm)
+ [Step 3: Purchase the Perpetual License or Subscription](#license-purchase)
+ [Step 4: Modify the License File](#setting-up-production-license-file)
+ [Step 5: Configure the RLM Server](#setting-up-rlm-server)
+ [Step 6: Configure the NICE DCV Server](#setting-up-dcv-server)

## Step 1: Install the RLM Server<a name="install-rlm"></a>

When you purchase a perpetual license or subscription, you get a license file that defines the terms of your license\. You must install the license file on a Reprise License Manager \(RLM\) server\. 

For more information about RLM, see the [Reprise Software](http://www.reprisesoftware.com/products/license-manager.php) website\.

**Topics**
+ [Install the RLM Server on Windows](#install-rlm-windows)
+ [Install the RLM Server on Linux](#install-rlm-linux)

### Install the RLM Server on Windows<a name="install-rlm-windows"></a>

**To install the RLM server on Windows**

1. Download the RLM License Administration Bundle from the [Reprise Software website](http://www.reprisesoftware.com/admin/software-licensing-download.php)\.

1. Install the RLM License Administration Bundle to `C:\RLM`\.

### Install the RLM Server on Linux<a name="install-rlm-linux"></a>

**To install the RLM server on Linux**

1. Download the RLM License Administration Bundle from the [Reprise Software website](http://www.reprisesoftware.com/admin/software-licensing-download.php)\.

1. Create a user group and an `rlm` user\. This can be any valid user or service account\. We strongly recommend that you do not use the root account for this value\.

   ```
   $ groupadd -r rlm
   ```

   ```
   $ useradd -r -g rlm -d "/opt/nice/rlm" -s /sbin/nologin -c "RLM License Server" rlm
   ```

1. Create the `/opt/nice/rlm` and `/opt/nice/rlm/license` directories required for the RLM server\.

   ```
   $ mkdir -p /opt/nice/rlm/license
   ```

1. Extract the contents of the RLM License Administration Bundle to `/opt/nice/rlm/`, and ensure that the files are owned by the `rlm` user\.

   ```
   $ tar xvf x64_l1.admin.tar.gz -C /opt/nice/rlm/ --strip-components 1
   ```

   ```
   $ chown -R rlm:rlm /opt/nice/rlm
   ```

## Step 2: Get the RLM Server's Host ID<a name="hostid-rlm"></a>

After you install the RLM server, you must get the RLM server's host ID\. You'll need to provide this host ID when purchasing a perpetual license or subscription\.

### Get the RLM Server Host ID on Windows<a name="hostid-rlm-windows"></a>

**To get the server's host ID, open the command prompt,**  
Navigate to `C:\RLM\`, and then run the following command\.

```
C:\> rlmutil.exe rlmhostid ether
```

The command returns the RLM server's host ID as follows\.

```
Hostid of this machine: 06814example
```

Record the host ID\. You need it for the next step\.

### Get the RLM Server Host ID on Linux<a name="hostid-rlm-linux"></a>

**To get the server's host ID**  
Navigate to `/opt/nice/rlm/`, and run the following command\.

```
$ ./rlmutil rlmhostid ether
```

The command returns the RLM server's host ID as follows\.

```
Hostid of this machine: 06814example
```

Record the host ID\. You need it for the next step\.

## Step 3: Purchase the Perpetual License or Subscription<a name="license-purchase"></a>

For information about how to purchase a NICE DCV perpetual license or a subscription, see [How to Buy](https://www.nice-software.com/index.html#buy) on the NICE website and find a NICE distributor or reseller in your region\.

You must provide your RLM server's host ID\. The host ID is embedded in the license file that NICE provides\.

## Step 4: Modify the License File<a name="setting-up-production-license-file"></a>

When you purchase a NICE DCV perpetual license or subscription, you receive a `license.lic` file that defines the license\. The `license.lic` file includes the following information:
+ The RLM server's hostname\.
+ The RLM server's host ID, which you provided when you purchased the license\.
+ The RLM server's TCP port number\. The default is `5053`\.
+ The ISV port number\. This is an optional port on which the RLM server listens for NICE DCV license requests\.
+ The NICE DCV products covered by the license, along with the following details for each product:
  + The major version covered by the license \(for example, `2017` for the 2017 NICE DCV products\)\.
  + The expiration date\. `Permanent` indicates that the license does not expire\.
  + The maximum number of concurrent sessions \(for example, `10` for 10 concurrent sessions on the server\)\.
  + The license checksum\.
  + The license signature\.

The following code block shows the format of the `license.lic` file:

```
HOST RLM_server_hostname RLM_server_host_id RLM_server_port
ISV nice port=port_number
LICENSE product_1 major_version expiration_date concurrent_sessions share=hi _ck=checksum sig="signature"
LICENSE product_2 major_version expiration_date concurrent_sessions share=hi _ck=checksum sig="signature"
```

The following code block shows an example of a `license.lic` file with the ISV port omitted\. The license file includes licenses for two NICE products, DCV and dcv\-gl\.

```
HOST My-RLM-server abcdef123456 5053
ISV nice
LICENSE nice dcv 2017 permanent 10 share=hi _ck=456789098a sig="abcdefghijklmnopqrstuvwxyz1234567890abcdefghijklmnopqrstuvwxyz1234567890ab"
LICENSE nice dcv-gl 2017 permanent 10 share=hi _ck=123454323x sig="1234567890abcdefghijklmnopqrstuvwxyz1234567890abcdefghijklmnopqrstuvwxyz12"
```

**To edit the `license.lic` file**

1. Open the file with your preferred text editor\.

1. Add your RLM server's hostname and the TCP port number to the first line in the file, which starts with `HOST`\.
**Warning**  
The *RLM\_server\_host\_id* is the host ID that you provided when you purchased the license\. You cannot edit the *RLM\_server\_host\_id*\.

1. \(Optional\) Add the ISV port number in the second line in the file, which starts with `ISV`, by adding `port=port_number`\.

   If you do not want to specify an ISV port, omit `port=port_number`\. If you do not specify a port, a random port is used\. Using a random port might cause conflicts with your firewall configuration\.

1. Save and close the file\.

**Warning**  
Editing any other part of the license file corrupts the file's signature and invalidates the license\.

## Step 5: Configure the RLM Server<a name="setting-up-rlm-server"></a>

After you have modified the license file, you must place it on your RLM server and then start the RLM service\.

**Topics**
+ [Configure the RLM Server on Windows](#prep-windows)
+ [Configure the RLM Server on Linux](#prep-linux)

### Configure the RLM Server on Windows<a name="prep-windows"></a>

**To configure the RLM server on Windows**

1. Connect to your RLM server\.

1. Copy the edited `license.lic` file to `C:\RLM\license\`\.

1. Copy the `C:\Program Files\NICE\DCV\Server\license\nice.set` file from your NICE DCV server and place it in the `C:\RLM\` folder on your RLM server\.

1. Install the RLM server as a Windows service\.

   ```
   C:\> rlm.exe -nows -dlog C:\RLM\rlm.log -c C:\RLM\license -install_service -service_name dcv-rlm
   ```

   For more information about the RLM startup options, see the [RLM License Administration Manual](http://www.reprisesoftware.com/RLM_Enduser.html)\.

1. Start the RLM server\.

   ```
   C:\> net start dcv-rlm
   ```

1. Confirm that the RLM server is running\.

   1. Open `C:\RLM\nice.dlog` with your preferred text editor and confirm that the following line appears\.

      ```
      date_time (nice) Server started on license1 (hostid: host_id) for: dcv dcv-gl
      ```
**Note**  
The contents of the `rlm.log` file might vary slightly depending on the RLM server version\.

   1. Run the following command\.

      ```
      C:\RLM\rlmutil rlmstat -a -c rlm_server_hostname@5053
      ```

      The command should return information about the RLM server\.

### Configure the RLM Server on Linux<a name="prep-linux"></a>

**To configure the RLM server on Linux**

1. Copy the edited `license.lic` file to `/opt/nice/rlm/license/`\.

1. Copy the `/usr/share/dcv/license/nice.set` file from your NICE DCV server and place it in `/opt/nice/rlm` on your RLM server\.

1. Create an RLM server service and make sure that it starts automatically at startup\.

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

1. Start the RLM server:

   ```
   $ service dcv-rlm start
   ```

1. Verify that the RLM server is running and functioning as expected\. Open `var/log/rlm.log` with your preferred text editor and confirm that the following line appears:

   ```
   date_time (nice) Server started on license1 (hostid: host_id) for: dcv dcv-gl
   ```
**Note**  
The contents of the `rlm.log` file might vary slightly depending on the RLM server version\.

## Step 6: Configure the NICE DCV Server<a name="setting-up-dcv-server"></a>

Configure your NICE DCV server to use the RLM server\. To do this, you must configure the `license-file` configuration parameter on your NICE DCV server\.

**Topics**
+ [Windows NICE DCV Server Configuration](#config-win)
+ [Linux NICE DCV Server Configuration](#config-linux)

### Windows NICE DCV Server Configuration<a name="config-win"></a>

**To configure the `license-file` configuration parameter on a Windows server**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/license/** key and select the **license\-file** parameter\.

   If there is no `license-file` parameter in the registry key, you must create it:

   1. Open the context \(right\-click\) menu for the **license** key in the left pane and choose **New**, **String Value**\.

   1. For **Name**, enter `license-file` and press **Enter**\.

1. Open the **license\-file** parameter\. For **Value data**, enter the RLM server's port number and hostname in the `5053@RLM_server_hostname` format\.
**Note**  
You can use the RLM server IP address instead of its hostname\.

1. Choose **OK** and close the Windows Registry Editor\.

### Linux NICE DCV Server Configuration<a name="config-linux"></a>

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