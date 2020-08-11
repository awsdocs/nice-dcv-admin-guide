# Prerequisites for Windows NICE DCV Servers on Amazon EC2 Instances<a name="setting-up-installing-winprereq"></a>

This topic explains how to configure your Windows Amazon EC2 instance before you install the NICE DCV server\. If you're not installing the NICE DCV server on an Amazon EC2 Windows instance, skip these prerequisites\.

**Topics**
+ [Prerequisites for Accelerated Computing Instances](#setting-up-installing-graphics)
+ [Prerequisites for Other Instance Families](#setting-up-installing-general)

## Prerequisites for Accelerated Computing Instances<a name="setting-up-installing-graphics"></a>

### Prerequisites for GPU Graphics Instances<a name="setting-up-installing-graphics"></a>

If you're using a GPU graphics instance, such as G2, G3, or G4, we recommend that you install and configure the appropriate NVIDIA GPU drivers\. The NVIDIA GPU drivers enable the following:
+ DirectX and OpenGL hardware acceleration for applications
+ Hardware acceleration for H\.264 video streaming encoding
+ Customizable server monitor resolutions
+ Increased maximum resolution for server monitors— up to 4096x2160
+ Increased number of server monitors

For more information about installing NVIDIA GPU drivers on your GPU graphics instance, see [ Installing the NVIDIA Driver on Windows](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/install-nvidia-driver.html) in the *Amazon EC2 User Guide for Windows Instances*\.

### Prerequisites for Other Accelerated Computing Instances<a name="setting-up-installing-accelerated"></a>

If you're using an accelerated computing instance that is not a GPU graphics instance, such as P2, P3, or P3dn, we recommend that you install and configure the appropriate NVIDIA GPU drivers\. The NVIDIA GPU drivers enable hardware acceleration for H\.264 video streaming encoding\.

For more information about installing NVIDIA GPU drivers on your accelerated computing instance, see [ Public NVIDIA Drivers](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/install-nvidia-driver.html#public-nvidia-driver) in the *Amazon EC2 User Guide for Windows Instances*\.

Unlike the GPU graphics instance, installing the NVIDIA GPU drivers on an accelerated computing instance does not enhance server monitor limits or resolutions in any way\. To add the additional server monitor resolution support, you can install the NVIDIA GRID drivers\. For more information, see [NVIDIA vGPU Software](https://www.nvidia.com/object/vGPU-software-driver.html) on the NVIDIA website\.

## Prerequisites for Other Instance Families<a name="setting-up-installing-general"></a>

For instances other than accelerated computing instances, such as instances in the general purpose, compute\-optimized, memory\-optimized, and storage\-optimized instance families, we recommend that you install the NICE DCV Virtual Display driver\.

Installing the NICE DCV Virtual Display driver does the following:
+ Increases the maximum number of server monitors to four\.
+ Enables custom server monitor resolutions\.
+ Increases maximum supported server monitor resolution to 4K\.

Server monitors attached by the NICE DCV server can't be managed by using Windows Control Panel\.

**Note**  
The NICE DCV Virtual Display driver is supported on Windows Server 2012 R2 and later\.

**Important**  
Installing the NICE DCV Virtual Display driver with any other GPU drivers, such as NVIDIA GPU drivers, might cause conflicts\. To avoid conflicts, we recommend that you do not install the NICE DCV Virtual Display driver with any other GPU drivers\.

**To install the NICE DCV Virtual Display driver on your instance**

1. Download the NICE DCV Virtual Display driver installer from the [NICE DCV website](https://download.nice-dcv.com/)\.

1. To install the driver by running the wizard, open or double\-click the installation file\. Or, use the following command to run an unattended installation\.

   ```
   C:\> nice-dcv-virtual-display-x64-Release-34.msi /quiet /norestart
   ```

1. Reboot the instance, and then reconnect to it\.