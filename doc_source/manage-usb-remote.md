# Enabling USB Remotization<a name="manage-usb-remote"></a>

NICE DCV enables clients to use specialized USB devices, such as 3D pointing devices or graphic tablets\. The devices are physically connected to their computer to interact with an application running on a NICE DCV server\.

**Note**  
USB remotization is only supported with the Windows client\. It is not supported with the portable Windows client or the web browser client\. Additional configuration might be required on the NICE DCV client\. For more information, see [Using USB Remotization](https://docs.aws.amazon.com/dcv/latest/userguide/using-usb.html) in the *NICE DCV User Guide*\.

The NICE DCV server uses a *whitelist* to determine which USB devices clients are allowed to use\. Some commonly used USB devices are added to the whitelist by default\. This enables clients to connect these USB devices to their computer and use them on the server without any additional configuration\.

However, some specialized devices might not be whitelisted by default\. These devices must be manually added to the whitelist on the NICE DCV server before they can be used by the client\. After they have been added to the whitelist, they appear in the Windows client **Settings** menu\.

## Whitelisting USB devices on a Windows NICE DCV Server<a name="manage-usb-remote-windows"></a>

To add a USB device to the whitelist, you must obtain the USB device's filter string from the client and add it to the `usb-devices.conf` file\.

**To add a USB device to the whitelist on a Windows NICE DCV server**

1. Ensure that you have installed the latest version of the NICE DCV server, and that you opted to install the USB remotization drivers\. For more information, see [Installing the NICE DCV Server on Windows](setting-up-installing-windows.md)\.

1. Install the USB device's hardware drivers on the NICE DCV server\.

1. Request the filter string from the client\. For more information, see [Using USB Remotization](https://docs.aws.amazon.com/dcv/latest/userguide/using-usb.html) in the *NICE DCV User Guide*\.

1. Open `C:\Program Files\NICE\DCV\Server\conf\usb-devices.conf` using your preferred text editor and add the filter string to a new line at the bottom of the file\.

1. Save and close the file\.

1. [Stop](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-stop.html) and [restart](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-start.html) the NICE DCV server\.

## Whitelisting USB devices on a Linux NICE DCV Server<a name="manage-usb-remote-linux"></a>

To add a USB device to the whitelist, you must obtain the USB device's filter string from the client and add it to the `usb-devices.conf` file\.

**Adding USB devices to the whitelist on a Linux NICE DCV server**

1. Ensure that you have installed the latest version of the NICE DCV server and the DCV USB driver\. For more information, see [Installing the NICE DCV Server on Linux](setting-up-installing-linux.md)\.

1. Install the USB device's hardware drivers on the NICE DCV server\.

1. Request the filter string from the client\. For more information, see [Using USB Remotization](https://docs.aws.amazon.com/dcv/latest/userguide/using-usb.html) in the *NICE DCV User Guide*\.

1. Open `/etc/dcv/usb-devices.conf` using your preferred text editor and add the filter string to a new line at the bottom of the file\.

1. Save and close the file\.

1. [Stop](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-stop.html) and [restart](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-start.html) the NICE DCV server\.