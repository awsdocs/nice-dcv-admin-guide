# Enabling USB remotization<a name="manage-usb-remote"></a>

With NICE DCV, clients can use a variety of specialized USB devices, such as 3D pointing devices or authentication devices\. The devices are physically connected to their computer to interact with an application that are running on a NICE DCV server\.

**Important**  
NICE DCV provides a generic mechanism for redirecting USB devices\. Some devices that are sensitive to network latency might experience issues\. Additionally, some devices might not function as expected due to driver compatibility issues\. Ensure that your devices work as expected before deploying to production\.

**Note**  
USB remotization is only supported with the Windows client\. It's not supported with the portable Windows client or the web browser client\. Additional configuration might be required on the NICE DCV client\. For more information, see [Using USB Remotization](https://docs.aws.amazon.com/dcv/latest/userguide/using-usb.html) in the *NICE DCV User Guide*\.

The NICE DCV server uses an allow list to determine which USB devices clients are allowed to use\. By default, some commonly used USB devices are added to the allow list\. This means clients can connect these USB devices to their computer and use them on the server without any additional configuration\.

However, some specialized devices might not be added to the allow list by default\. These devices must be manually added to the allow list on the NICE DCV server before they can be used by the client\. After they have been added, they appear in the Windows client **Settings** menu\.

------
#### [ Windows NICE DCV server ]

To add a USB device to the allow list, you must obtain the USB device's filter string from the client and add it to the `usb-devices.conf` file\.

**To add a USB device to the allow list on a Windows NICE DCV server**

1. Ensure that you have installed the latest version of the NICE DCV server and that you opted to install the USB remotization drivers\. For more information, see [Installing the NICE DCV Server on Windows](setting-up-installing-windows.md)\.

1. Install the USB device's hardware drivers on the NICE DCV server\.

1. Request the filter string from the client\. For more information, see [Using USB Remotization](https://docs.aws.amazon.com/dcv/latest/userguide/using-usb.html) in the *NICE DCV User Guide*\.

1. Open `C:\Program Files\NICE\DCV\Server\conf\usb-devices.conf` using your preferred text editor and add the filter string to a new line at the bottom of the file\.

1. Save and close the file\.

1. [Stop](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-stop.html) and [restart](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-start.html) the NICE DCV server\.

------
#### [ Linux NICE DCV server ]

To add a USB device to the allow list, add the filter string for the USB device to the `usb-devices.conf` file\.

**Adding USB devices to the allow list on a Linux NICE DCV server**

1. Ensure that you have installed the latest version of the NICE DCV server and the DCV USB driver\. For more information, see [Installing the NICE DCV Server on Linux](setting-up-installing-linux.md)\.

1. Install the USB device's hardware drivers on the NICE DCV server\.

1. Request the filter string from the client\. For more information, see [Using USB Remotization](https://docs.aws.amazon.com/dcv/latest/userguide/using-usb.html) in the *NICE DCV User Guide*\.

1. Open `/etc/dcv/usb-devices.conf` using your preferred text editor and add the filter string to a new line at the bottom of the file\.

1. Save and close the file\.

1. [Stop](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-stop.html) and [restart](https://docs.aws.amazon.com/dcv/latest/adminguide/manage-start.html) the NICE DCV server\.

------