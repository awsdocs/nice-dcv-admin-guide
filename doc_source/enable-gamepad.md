# Enabling gamepad support<a name="enable-gamepad"></a>

Beginning with NICE DCV Server 2022\.0, gamepad devices can be used when connecting to any of the supported Windows or Linux operating systems\.

The following gamepad devices are supported:
+ Xbox 360 controller
+ DualShock 4 controller

Other devices that are compatible with the devices listed above, or that can be configured to emulate one of the supported devices, may also work\.

**Note**  
Gamepad devices are supported only when using the Windows native NICE DCV client\. Ensure you are using NICE DCV Client 2022\.0 or newer\.

To enable gamepad support, ensure that you have installed the latest version of the NICE DCV Server and that you opted to install the Gamepad driver\. For more information, see [Installing the NICE DCV Server on Windows](setting-up-installing-windows.md)\. When the driver is installed, the feature is enabled by default on Windows NICE DCV servers\.

## Supporting Xbox 360 controllers<a name="enable-gamepad-xbox"></a>

Xbox 360 controllers require the installation of their Windows driver\. This driver is not automatically installed on Windows and needs to be retrieved from the official windows update web site\.

**To download and install the Xbox 360 controller driver:**

1. Search for the driver on the Microsoft Update Catalog page: [https://www.catalog.update.microsoft.com/Search.aspx?q=game+devices+XBOX+360+Controller+For+Windows](https://www.catalog.update.microsoft.com/Search.aspx?q=game+devices+XBOX+360+Controller+For+Windows)\.

1. Download the newest version of the driver for your operating system\.

1. Open the \.cab file and extract its contents:

   ```
   expand filename.cab -F:*
   ```

1. Install the the \.inf file of the driver with the following command:

   ```
   pnputil /add-driver filename.inf /install
   ```