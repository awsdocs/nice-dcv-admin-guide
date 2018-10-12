# Enabling GPU Sharing on a Linux NICE DCV Server<a name="manage-gpu"></a>

GPU sharing enables you to share one or more physical GPUs between multiple NICE DCV virtual sessions\. For more information about sessions, see [Managing NICE DCV Sessions](managing-sessions.md)\. Using GPU sharing enables you to use a single NICE DCV server and host multiple virtual sessions that share the server's physical GPU resources\. 

**Note**  
GPU sharing is only supported on Linux NICE DCV servers\.

**Before You Begin**

Before you begin, ensure that the following prerequisites are completed:
+ Install the NICE DCV server on a Linux server\.
+ Install the NICE DCV `dcv-gl` and `nice-Xdcv` packages on the server\.
+ Ensure that the server has at least one supported NVIDIA GPU\.
+ Install the NVIDIA GPU driver on the server\. Official NVIDIA drivers are required\. The open\-source NVIDIA drivers are not supported\.
+ Ensure that the NVIDIA GPU driver supports hardware\-accelerated OpenGL\.
+ Install an X Server, and configure the `Device` and `Screen` sections in the `xorg.conf` file\.
**Note**  
You can use the `nvidia-xconfig` NVIDIA utility to automatically create an `xorg.conf` file and configure it for all the available NVIDIA GPUs\.

You can install the `nice-dcv-gltest` rpm package and run the test application to check whether the server is properly configured for GPU sharing\.

To enable GPU sharing on the NICE DCV server, you must configure the `gl-displays` parameter in the `dcv-gl.conf` file after you have completed the prerequisites listed above\.

**To enable GPU sharing on a Linux NICE DCV server**

1. Navigate to `/etc/dcv/` and open the `dcv.conf ` with your preferred text editor\.

1. Add the `[display/linux]` section and `gl-displays` parameter using the following format:

   ```
   [display/linux]
   gl-displays = [':xserver.screen_1',':xserver.screen_2']
   ```

   The following example shows the `gl-displays` parameter for two screens running on the default X Server session:

   ```
   [display/linux]
   gl-displays = [':0.0',':0.1']
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.