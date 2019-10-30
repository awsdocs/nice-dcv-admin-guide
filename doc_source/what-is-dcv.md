# What Is NICE DCV?<a name="what-is-dcv"></a>

NICE DCV is a high\-performance remote display protocol\. It lets you securely deliver remote desktops and application streaming from any cloud or data center to any device, over varying network conditions\. By using NICE DCV with Amazon EC2, you can run graphics\-intensive applications remotely on Amazon EC2 instances\. You can then stream the results to more modest client machines, which eliminates the need for expensive dedicated workstations\.

**Topics**
+ [How NICE DCV Works](#what-is-dcv-how)
+ [Features](#what-is-dcv-features)
+ [Requirements](#what-is-dcv-requirements)
+ [Pricing](#what-is-dcv-pricing)

## How NICE DCV Works<a name="what-is-dcv-how"></a>

To use NICE DCV, install the NICE DCV server software on a server\. The NICE DCV server software is used to create a secure [session](https://docs.aws.amazon.com/dcv/latest/adminguide/managing-sessions.html)\. You install and run your applications on the server\. The server uses its hardware to perform the high\-performance processing that the installed applications require\. Your users access the application by remotely connecting to the session using a NICE DCV client application\. When the connection is established, the NICE DCV server software compresses the visual output of the application and streams it back to the client application in an encrypted pixel stream\. The client application receives the compressed pixel stream, decrypts it, and then outputs it to the local display\.

## Features of NICE DCV<a name="what-is-dcv-features"></a>

NICE DCV offers the following features:
+ **Shares the entire desktop** — Uses the high\-performance NICE DCV protocol to share full control of the entire remote desktop\.
+ **Transport images only** — Transports rendered images as pixels instead of geometry and scene information\. This provides an additional layer of security as no proprietary customer information is sent over the network\.
+ **Supports H\.264\-based encoding** — Uses H\.264\-based video compression and encoding to reduce bandwidth consumption\. 
+ **Supports lossless quality video compression** \- Supports lossless quality video compression when the network and processor conditions allow\.
+ **Matches display layouts** — Automatically adapts the server's screen resolution and display layout to match the size of the client window\.
+ **Supports multi\-screen** — Lets you expand the session desktop across up to four monitors\.
+ **Adapts compression levels** — Automatically adapts the video compression levels based on the network's available bandwidth and latency\.
+ **Enables collaboration** — Provides dynamic sessions that support multiple collaborative clients\. Clients can connect and disconnect at any time during the session\. 
+ **Supports multiple sessions per server** \(Linux NICE DCV servers only\) — Supports multiple virtual sessions per Linux NICE DCV server to maximize cost savings\.
+ **Supports GPU sharing** \(Linux NICE DCV servers only\) — Lets you share one or more physical GPUs between multiple virtual sessions running on a Linux NICE DCV server\.
+ **Supports USB, smart card, and stylus remotization** — Lets you use your peripherals in a NICE DCV session just like you would on your local computer\.
+ **Supports audio in and out, printing, and copy and paste** — Lets you perform these key actions between the session and your local computer\.
+ **Supports file transfer** — Lets you transfer files between the session and your local computer\.
+ **Provides an HTML5 client** \- Offers an HTML5 client that can be used with any modern web browser on Windows and Linux\.
+ **Supports modern Linux desktop environments** — Supports modern Linux desktops, such as Gnome 3 on RHEL 7\.

## NICE DCV Requirements<a name="what-is-dcv-requirements"></a>

For a good user experience with NICE DCV, ensure that the server and client computers meet the following minimum requirements\. Keep in mind that your users' experience is largely dependent on the number of pixels streamed from the NICE DCV server to the NICE DCV client\.

**Contents**
+ [Server Requirements](#what-is-dcv-requirements-server)
+ [Client Requirements](#what-is-dcv-requirements-client)

### NICE DCV Server Requirements<a name="what-is-dcv-requirements-server"></a>

If you are installing the NICE DCV server on an Amazon EC2 instance, we recommend that you use an Amazon EC2 G3 or G4 instance type\. These instance types offer NVIDIA GPUs that support hardware\-based OpenGL and GPU sharing\. For more information, see [Amazon EC2 G3 Instances](https://aws.amazon.com/ec2/instance-types/g3/) and [Amazon EC2 G4 Instances](https://aws.amazon.com/ec2/instance-types/g4/)\. You can install the NICE DCV server on any other instance type, but there might be screen resolution limitations\. A third\-party driver can be used to bypass this limitation\. If you need the third\-party driver, request it from [NICE Support\.](https://support.nice-software.com/support/login/)

NICE DCV servers must meet the minimum requirements listed in the following table\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html)

### NICE DCV Client Requirements<a name="what-is-dcv-requirements-client"></a>

The following table lists the minimum system requirements for the NICE DCV clients\.


|  | Native Windows client | Web browser client | Linux client | macOS client | 
| --- | --- | --- | --- | --- | 
| **Software** |  The Native Windows client is supported on 32\-bit and 64\-bit versions of the following operating systems: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html) The client also requires the following additional software: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html)  |  The web browser client is supported on the following browsers across all desktop operating systems: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html) The web browser client also requires WebGL and asm\.js\. The web browser client is not supported on mobile operating systems, such as Android and iOS\.  |  The Linux client is supported on the following modern Linux operating systems: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html)  |  The macOS client requires macOS High Sierra or later\.  | 
| **Network** | The client must be able to connect to the NICE DCV server, and it must be able to communicate over the required port \(8443 by default\)\. | 

## NICE DCV Pricing<a name="what-is-dcv-pricing"></a>

There is no additional charge for using the NICE DCV server on an Amazon EC2 instance\. You pay the standard rates for the instance and other Amazon EC2 features that you use\.

A license is required to install the NICE DCV server on an on\-premises or alternative cloud\-based server\. For more information, see [Licensing the NICE DCV Server](setting-up-license.md)\.