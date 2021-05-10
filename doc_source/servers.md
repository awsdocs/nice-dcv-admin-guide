# NICE DCV Servers<a name="servers"></a>

The NICE DCV server is available for Windows and Linux\. Both servers offer similar features, but there are some differences\. Choose the NICE DCV server that best meets your needs\. The following table compares the features supported by the Windows and Linux NICE DCV servers\.

**Topics**
+ [Requirements](#requirements)
+ [Supported Features](#features)

## Requirements<a name="requirements"></a>

For a good user experience with NICE DCV, ensure that your server meets the following minimum requirements\. Keep in mind that your users' experience is largely dependent on the number of pixels streamed from the NICE DCV server to the NICE DCV client\.

If you are installing the NICE DCV server on an Amazon EC2 instance, we recommend that you use an Amazon EC2 G3, G4dn, or G4ad instance type\. These instance types offer GPUs that support hardware\-based OpenGL and GPU sharing\. For more information, see [Amazon EC2 G3 Instances](https://aws.amazon.com/ec2/instance-types/g3/) and [Amazon EC2 G4 Instances](https://aws.amazon.com/ec2/instance-types/g4/)\. You can install the NICE DCV server on any other instance type, but there might be screen resolution limitations\. To bypass this limitation, download and install the [ NICE DCV Virtual Display Driver for EC2](https://d1uj6qtbmh3dt5.cloudfront.net/Drivers/nice-dcv-virtual-display-x64-Release-34.msi)\.

Your server must meet the minimum requirements listed in the following table\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/servers.html)

For more information about the NICE DCV Client requirements, see [ NICE DCV Client requirements](https://docs.aws.amazon.com/dcv/latest/userguide/client.html#requirements) in the *NICE DCV User Guide*\.

## Supported Features<a name="features"></a>

The following table compares the features that are supported by the WIndows and Linux NICE DCV serves\.


| Feature | [Windows NICE DCV server](setting-up-installing-windows.md) | [Linux NICE DCV server](setting-up-installing-linux.md) | 
| --- | --- | --- | 
| [Console sessions](managing-sessions.md) | ✓ | ✓ | 
| [Virtual sessions](managing-sessions.md) | ✗ | ✓ | 
| [Custom TCP port](manage-port.md) | ✓ | ✓ | 
| [Idle client disconnection](manage-disconnect.md) | ✓ | ✓ | 
| [GPU sharing](manage-gpu.md) | ✗ | ✓ | 
| [Custom TLS certificates](manage-cert.md) | ✓ | ✓ | 
| [USB remotization](manage-usb-remote.md) | ✓ | ✓ | 
| [Smart card support](manage-smart-card.md) | ✓ | ✓ | 
| Webcam support | ✓ | ✗ | 
| [Session storage and file transfer](manage-storage.md) | ✓ | ✓ | 
| [Copying and pasting](manage-clipboard.md) | ✓ | ✓ | 
| [Custom HTTP headers](manage-headers.md) | ✓ | ✓ | 
| [Printing from sessions](manage-printer.md) | ✓ | ✓ | 
| [Stereo 2\.0 audio playback](manage-audio.md) | ✓ | ✓ | 
| [Surround sound audio playback](manage-audio.md) | ✓ \(up to 7\.1\) | ✓ \(up to 5\.1\) | 
| [Stereo 2\.0 audio recording](manage-audio.md) | ✓ | ✗ | 
| [Touchscreen support](enable-stylus.md) | ✓ \(Windows 8\.1 and Server 2012 and later\) | ✓ | 
| [Stylus support](enable-stylus.md) | ✓ \(Windows 10 and Server 2019\) | ✓ | 

For more information about the NICE DCV Client features, see [ NICE DCV Client features](https://docs.aws.amazon.com/dcv/latest/userguide/client.html#client-features) in the *NICE DCV User Guide*\.