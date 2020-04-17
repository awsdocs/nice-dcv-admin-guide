# Enabling GPU Sharing on a Linux NICE DCV Server<a name="manage-gpu"></a>

GPU sharing enables you to share one or more physical GPUs between multiple NICE DCV virtual sessions\. For more information about sessions, see [Managing NICE DCV Sessions](managing-sessions.md)\. Using GPU sharing enables you to use a single NICE DCV server and host multiple virtual sessions that share the server's physical GPU resources\. 

**Note**  
GPU sharing is only supported on Linux NICE DCV servers\.

**Prerequisites**

Before you begin, complete the following prerequisites:
+ Install the NICE DCV server on a Linux server\.
+ Install the NICE DCV `dcv-gl` and `nice-Xdcv` packages on the server\.
+ Ensure that the server has at least one supported NVIDIA GPU\.
+ Install the NVIDIA GPU driver on the server\. Official NVIDIA drivers are required\. The open\-source NVIDIA drivers are not supported\.
+ Ensure that the NVIDIA GPU driver supports hardware\-accelerated OpenGL\.
+ Install an X Server and configure the `Device` and `Screen` sections in the `xorg.conf` file\.
**Note**  
You can use the `nvidia-xconfig` NVIDIA utility to automatically create an `xorg.conf` file and configure it for all the available NVIDIA GPUs\.
+ Ensure that the X Server is running\.
+ \(Optional\) Verify the NICE DCV server configuration by running the `dcvgldiag` tool\. For more information, see [Post\-Installation Checks](setting-up-installing-linux-checks.md)\.

  You can also install the `nice-dcv-gltest` package and run the `dcvgltest` test application to check whether the server is properly configured for GPU sharing\.

To enable GPU sharing, you must specify the list of GPUs to be used by the virtual sessions\. If you do not specify the GPUs, only the GPU used by the standard X Server, with the display name `:0.0`, is used\.

You must specify the GPUs in the `gl-displays` parameter in the `dcv.conf` file after you complete the prerequisites described earlier in this topic\.

**To enable GPU sharing on a Linux NICE DCV server**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` file with your preferred text editor\.

1. Add the `[display/linux]` section and the `gl-displays` parameter, and then specify the available GPUs in the following format:

   ```
   [display/linux]
   gl-displays = [':xserver_port.screen_number_1',':xserver_port.screen_number_2', ...]
   ```

   Where *xserver\_port* is the server and *screen\_number* is the number associated with the screen that is associated with the GPU\. *screen\_number* starts from `0`\.

   The following example shows the `gl-displays` parameter for two GPUs running on the default X Server session:

   ```
   [display/linux]
   gl-displays = [':0.0',':0.1']
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.