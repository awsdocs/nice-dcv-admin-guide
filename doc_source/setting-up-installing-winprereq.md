# Prerequisites for Windows NICE DCV server on Amazon EC2 instances<a name="setting-up-installing-winprereq"></a>

This topic describes how to configure your Windows Amazon EC2 instance before you install the NICE DCV server\. If you're not installing the NICE DCV server on an Amazon EC2 Windows instance, skip these prerequisites\.

**Topics**
+ [Prerequisites for accelerated computing instances](#setting-up-installing-graphics)
+ [Prerequisites for other instance families](#setting-up-installing-general)

## Prerequisites for accelerated computing instances<a name="setting-up-installing-graphics"></a>

### Prerequisites for GPU graphics instances<a name="setting-up-installing-graphics"></a>

If you're using a GPU graphics instance \(for example, a G2, G3, G4dn, or G4ad instance\), we recommend that you install and configure the appropriate NVIDIA or AMD GPU drivers\. The GPU drivers allow for the following:
+ DirectX and OpenGL hardware acceleration for applications
+ Hardware acceleration for H\.264 video streaming encoding
+ Customizable server monitor resolutions
+ Increased maximum resolution for server monitors— up to 4096x2160
+ Increased number of server monitors

For instructions on how to install NVIDIA GPU drivers on your GPU graphics instance, see the following topics in the *Amazon EC2 User Guide*\.
+ For instances with an NVIDIA GPU \(for example, a G2, G3, or G4dn instance\), see [ Installing the NVIDIA Driver on Windows](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/install-nvidia-driver.html)\.
+ For instances with an AMD GPU \(for example, a G4ad instance\), see [ Install AMD drivers on Windows instances](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/install-amd-driver.html)\.

For more information about Amazon EC2 G4ad instances, see the [Deep dive on the new Amazon EC2 G4ad instances ](http://aws.amazon.com/blogs/compute/deep-dive-on-the-new-amazon-ec2-g4ad-instances/) blog post\.

### Prerequisites for other accelerated computing instances<a name="setting-up-installing-accelerated"></a>

If you're using an accelerated computing instance that isn't a GPU graphics instance \(for example a P2, P3, or P3dn instance\), we recommend that you install and configure the appropriate NVIDIA GPU drivers\. The NVIDIA GPU drivers enable hardware acceleration for H\.264 video streaming encoding\.

For instructions on how to install NVIDIA GPU drivers on your accelerated computing instance, see [ Public NVIDIA Drivers](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/install-nvidia-driver.html#public-nvidia-driver) in the *Amazon EC2 User Guide for Windows Instances*\.

Installing the NVIDIA GPU drivers on an accelerated computing instance doesn't enhance server monitor limits or resolutions\. To add the additional server monitor resolution support, you can install the NVIDIA GRID drivers\. For more information, see [NVIDIA vGPU Software](https://www.nvidia.com/object/vGPU-software-driver.html) on the NVIDIA website\.

## Prerequisites for other instance families<a name="setting-up-installing-general"></a>

For instances other than accelerated computing instances, we recommend that you install the NICE DCV Virtual Display driver\. This includes instances in the general purpose, compute\-optimized, memory\-optimized, and storage\-optimized instance families\. 

Installing the NICE DCV Virtual Display driver enables the following:
+ Support for up to four monitors
+ Support for custom resolutions
+ Support for 4K UHD resolution

You can't manage server monitors attached by the NICE DCV server using Windows Control Panel\.

**Note**  
The NICE DCV Virtual Display driver is supported on Windows Server 2012 R2 and later\.

**Important**  
Installing the NICE DCV Virtual Display driver with any other GPU drivers, such as NVIDIA GPU drivers, might cause conflicts\. To avoid conflicts, we recommend that you don't install the NICE DCV Virtual Display driver in combination with any other GPU drivers\.

**To install the NICE DCV Virtual Display driver on your instance**

1. Download the NICE DCV Virtual Display driver installer from the [NICE DCV website](https://download.nice-dcv.com/)\.

1. To install the driver by running the wizard, open or double\-click the installation file\. Or, use the following command to run an unattended installation\.

   ```
   C:\> nice-dcv-virtual-display-x64-Release-34.msi /quiet /norestart
   ```

1. Reboot the instance, and then reconnect to it\.