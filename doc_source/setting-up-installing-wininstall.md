# Installing the NICE DCV Server on Windows<a name="setting-up-installing-wininstall"></a>

You can use an installation wizard to install the NICE DCV server on a Windows host server\. The wizard walks you through a series of steps that let you customize your NICE DCV server installation\. Or, you can use the command line to perform an unattended installation, which uses default settings to automate the installation procedure\.

**Note**  
The NICE DCV server installer is signed by an SHA\-256 certificate\. If you are using a server running Windows 7 or Windows Server 2008 R2, you must install a Microsoft security update to support this certificate type\. For more information, see [Microsoft Security Advisory 3033929](https://docs.microsoft.com/en-us/security-updates/SecurityAdvisories/2015/3033929) and [Microsoft Windows Support](https://support.microsoft.com/en-us/help/2921916/the-untrusted-publisher-dialog-box-appears-when-you-install-a-driver-i)\.

**Contents**
+ [Using the Wizard](#setting-up-installing-windows-wizard)
+ [Unattended Installation](#setting-up-installing-windows-unattended)

## Using the Wizard<a name="setting-up-installing-windows-wizard"></a>

Use the NICE DCV server installation wizard for a guided installation\.

**To install the NICE DCV server on Windows using the wizard**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. Download the NICE DCV server installer from the [NICE](http://download.nice-dcv.com) website\.
**Note**  
The NICE DCV server is available only in a 64\-bit version and supported on 64\-bit Windows operating systems\.

1. Run `nice-dcv-server-x64-Release-2020.1-version_number.msi`\. 

1. On the Welcome screen, choose **Next**\.

1. On the End\-User License Agreement screen, read the license agreement\. If you accept the terms, select the **I accept the terms in the License Agreement** check box, and then choose **Next**\.

1. \(Optional\) On the **Drivers Selection** screen, select **USB device remotization**, and choose **Will be installed on local hard drive**, **Next**\. This installs the drivers required to support some specialized USB devices, such as 3D pointing devices and graphic tablets\.

1. On the DCV Service Configuration screen:

   1. \(Optional\) To manually configure your server's firewall to allow communication over the required port, select **No, I will manually configure my firewall later**\.

   1. \(Optional\) To manually start the NICE DCV server after the installation, select **No, I want to start a DCV Service manually**\. If you select this option, you can't start a console session automatically after the installation is complete\. If you select this option, step 9 is skipped\.

1. Choose **Next**\.

1. On the DCV Session Management Configuration screen, specify the owner for the automatic console session\. Or, to prevent the automatic console session from starting after the installation is complete, select **No, I will create the session manually**\.
**Note**  
Complete this step only if you previously chose to allow the server to start automatically\.

1. Choose **Install**\.

## Unattended Installation<a name="setting-up-installing-windows-unattended"></a>

The unattended installation does the following by default:
+ Adds a firewall rule to allow communication over port 8443\.
+ Enables NICE DCV server auto\-start\.
+ Creates an automatic console session\.
+ Sets the console session owner to the user who performs the installation\.

You can override the default actions by appending the following options to the installation command:
+ `DISABLE_FIREWALL=1` — Prevents the installer from adding the firewall rule\.
+ `DISABLE_SERVER_AUTOSTART=1` — Prevents the NICE DCV server from starting automatically after the installation\.
+ `DISABLE_SERVER_AUTOMATIC_SESSION_CREATION=1` — Prevents the installer from starting the automatic console session\.
+ `AUTOMATIC_SESSION_OWNER=owner_name` — Specifies a different owner for the automatic console session\.
+ `ADDLOCAL=ALL` — Installs the DCV drivers required for USB remotization\.

**To install the NICE DCV server on Windows using an unattended installation**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. Download the NICE DCV server installer from the [NICE](http://download.nice-dcv.com) website\.
**Note**  
The NICE DCV server is available only in a 64\-bit version and supported on 64\-bit Windows operating systems\.

1. Open a command prompt window and navigate to the folder where you downloaded the installer\.

1. Run the unattended installer:

   ```
   C:\> msiexec.exe /i nice-dcv-server-x64-Release-2020.1-version_number.msi /quiet /norestart /l*v dcv_install_msi.log
   ```