# Installing the NICE DCV Server on Windows<a name="setting-up-installing-wininstall"></a>

You can use an installation wizard to install the NICE DCV server on a Windows host server\. The wizard guides you through a series of steps that show how to customize your NICE DCV server installation\. Alternatively, you can use the command line to perform an unattended installation\. This uses default settings to automate the installation procedure\.

**Contents**
+ [Using the wizard](#setting-up-installing-windows-wizard)
+ [Unattended installation](#setting-up-installing-windows-unattended)

## Using the wizard<a name="setting-up-installing-windows-wizard"></a>

Use the NICE DCV server installation wizard for a guided installation\.

**To install the NICE DCV server on Windows using the wizard**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. Download the NICE DCV server installer from the [NICE](http://download.nice-dcv.com) website\.
**Note**  
The NICE DCV server is available only in a 64\-bit version and supported on 64\-bit Windows operating systems\.

1. Run `nice-dcv-server-x64-Release-2021.2-version_number.msi`\. 

1. On the Welcome screen, choose **Next**\.

1. On the End\-User License Agreement screen, read the license agreement\. If you accept the terms, select the **I accept the terms in the License Agreement** check box, and then choose **Next**\.

1. \(Optional\) On the **Drivers Selection** screen, select **USB device remotization**, and choose **Will be installed on local hard drive**, **Next**\. This installs the drivers required to support some specialized USB devices\. Examples include 3D pointing devices and graphic tablets\.

1. On the DCV Service Configuration screen:

   1. \(Optional\) To manually configure your server's firewall to allow communication over the required port, select **No, I will manually configure my firewall later**\.

   1. \(Optional\) To manually start the NICE DCV server after the installation, select **No, I want to start a DCV Service manually**\. If you select this option, you can't start a console session automatically after the installation is complete\. If you select this option, step 9 is skipped\.

1. Choose **Next**\.

1. On the DCV Session Management Configuration screen, specify the owner for the automatic console session\. Or, to prevent the automatic console session from starting after the installation is complete, select **No, I will create the session manually**\.
**Note**  
Complete this step only if you previously chose to allow the server to start automatically\.

1. Choose **Install**\.

## Unattended installation<a name="setting-up-installing-windows-unattended"></a>

By default, the unattended installation does the following:
+ Adds a firewall rule to allow communication over port 8443\.
+ Enables NICE DCV server auto\-start\.
+ Creates an automatic console session\.
+ Sets the console session owner to the user who performs the installation\.

You can override the default actions by appending the following options to the installation command:
+ `DISABLE_FIREWALL=1` — Prevents the installer from adding the firewall rule\.
+ `DISABLE_SERVER_AUTOSTART=1` — Prevents the NICE DCV server from starting automatically after the installation\.
+ `DISABLE_AUTOMATIC_SESSION_CREATION=1` — Prevents the installer from starting the automatic console session\.
+ `AUTOMATIC_SESSION_OWNER=owner_name` — Specifies a different owner for the automatic console session\.
+ `ADDLOCAL=component_list` — Adds elements to the set of elements to be installed\.
+ `REMOVE=component_list` — Removes elements from the set of elements to be installed\.
**Note**  
The `REMOVE` option is evaluated after the `ADDLOCAL` option\. An element that's on both lists isn't installed\.

The component\_list is a comma\-separated list that can contain the following values:
+ `audioMicDriver`: Microphone driver
+ `audioSpkDriver`: Speaker driver
+ `printerDriver`: Printer driver
+ `usbDriver`: USB device remotization driver \(Disabled by default\)
+ `webcamDriver`: Webcam driver
+ `webClient`: Web client
+ `ALL`: All components

**To install the NICE DCV server on Windows using an unattended installation**

1. Launch and connect to the server that you intend to install the NICE DCV server on\.

1. Download the NICE DCV server installer from the [NICE](http://download.nice-dcv.com) website\.
**Note**  
The NICE DCV server is available only in a 64\-bit version and supported on 64\-bit Windows operating systems\.

1. Open a command prompt window and navigate to the folder where you downloaded the installer\.

1. Run the unattended installer as seen in one of the following examples:
   + Install default components:

     ```
     C:\>  msiexec.exe /i nice-dcv-server-x64-Release-2021.2-version_number.msi 
     /quiet /norestart /l*v dcv_install_msi.log
     ```
   + Install all components:

     ```
     C:\>  msiexec.exe /i nice-dcv-server-x64-Release-2021.2-version_number.msi 
     ADDLOCAL=ALL /quiet /norestart /l*v dcv_install_msi.log
     ```
   + Install a subset of components:

     ```
     C:\>  msiexec.exe /i nice-dcv-server-x64-Release-2021.2-version_number.msi 
     ADDLOCAL=audioMicDriver,audioSpkDriver,printerDriver,webcamDriver /quiet /norestart /l*v dcv_install_msi.log
     ```