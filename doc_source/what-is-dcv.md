# What Is NICE Desktop Cloud Visualization?<a name="what-is-dcv"></a>

NICE Desktop Cloud Visualization is a remote visualization technology that enables users to securely connect to graphic\-intensive 3D applications hosted on a remote high\-performance server\. With NICE DCV, you can make a server's high\-performance graphics processing capabilities available to multiple remote users by creating secure client sessions\. This enables your users to use resource\-intensive applications with relatively low\-end client computers by using the server's processor, GPU, I/O capabilities, and memory\.

**Topics**
+ [How NICE DCV Works](#what-is-dcv-how)
+ [Features](#what-is-dcv-features)
+ [Requirements](#what-is-dcv-requirements)
+ [Pricing](#what-is-dcv-pricing)

## How NICE DCV Works<a name="what-is-dcv-how"></a>

In a typical NICE DCV scenario, a graphic\-intensive application, such as a 3D modeling or computer\-aided design application, is hosted on a high\-performance server that provides a high\-end GPU, fast I/O capabilities, and large amounts of memory\. The **NICE DCV server** software is installed and configured on the server and it is used to create a secure session\. You use a **NICE DCV client** to remotely connect to the session and use the application hosted on the server\. The server uses its hardware to perform the high\-performance processing required by the hosted application\. The **NICE DCV server** software compresses the visual output of the hosted application and streams it back to you as an encrypted pixel stream\. Your **NICE DCV client** receives the compressed pixel stream, decrypts it, and then outputs it to your local display\.

## Features of NICE DCV<a name="what-is-dcv-features"></a>

NICE DCV offers the following features:
+ **Enables collaboration** — It provides sessions that support multiple collaborative clients\. Sessions are dynamic and clients can connect and disconnect at any time during the session\. 
+ **Supports GPU sharing** \(Linux NICE DCV servers only\) — Enables you to share one or more physical GPUs between multiple virtual sessions running on a Linux NICE DCV server\.
+ **Supports H\.264\-based encoding** — It uses H\.264\-based video compression and encoding to reduce bandwidth consumption\. 
+ **Supports NVIDIA GRID** — It uses the latest NVIDIA Grid SDK technologies, such as NVIDIA H\.264 hardware encoding, to improve performance and reduce system load\. Requires an NVIDIA GRID compatible GPU\.
+ **Shares the entire desktop** — It uses the high\-performance NICE DCV protocol to share full control of the entire desktop\.
+ **Supports NVIDIA vGPU technology** — It uses the NVIDIA virtual GPU \(vGPU\) technology to simplify the deployment of Windows virtual machines and to support GPU sharing\. Requires an NVIDIA GRID compatible GPU\.
+ **Supports lossless quality video compression** \- It supports lossless quality video compression when the network and processor conditions allow\.
+ **Transport images only** — It transports rendered images as pixels instead of geometry and scene information\. This provides an additional layer of security as no proprietary customer information is sent over the network\.
+ **Adapts compression levels** — It automatically adapts the video compression levels based on the network's available bandwidth and latency\.
+ **Supports smart card remotization** — It provides seamless access to local smart cards using the Personal Computer/Smart Card \(PC/SC\) interface\. Smart cards can be used for encrypting emails, signing documents, and authenticating against remote systems\. Requires the native Windows NICE DCV client and a Linux NICE DCV server\.
+ **Matches display layouts** — It automatically adapts the server's screen resolution and display layout to match the size of the client window\.
+ **Provides an HTML5 client** \- It offers an HTML5 client that can be used with any modern web browser on Windows and Linux\.
+ **Supports modern Linux desktop environments** —It supports modern Linux desktops, such as Gnome 3 on RHEL 7\.

## NICE DCV Requirements<a name="what-is-dcv-requirements"></a>

For a good user experience with NICE DCV, ensure that the server and client computers meet the following minimum requirements\. Keep in mind that your users' experience is largely dependent on the number of pixels streamed from the NICE DCV server to the NICE DCV client\.

**Contents**
+ [Server Requirements](#what-is-dcv-requirements-server)
+ [Client Requirements](#what-is-dcv-requirements-client)

### NICE DCV Server Requirements<a name="what-is-dcv-requirements-server"></a>

If you are installing the NICE DCV server on an Amazon EC2 instance, we recommend that you use an Amazon EC2 G3 instance type\. These instance types offer NVIDIA GPUs that support hardware\-based OpenGL and GPU sharing\. For more information, see [Amazon EC2 G3 Instances](https://aws.amazon.com/ec2/instance-types/g3/)\. You can install the NICE DCV server on any other instance type, but there might be screen resolution limitations\. A third\-party driver can be used to bypass this limitation\. If you need the third\-party driver, request it from [NICE Support\.](https://support.nice-software.com/support/login/)

NICE DCV servers must meet the minimum requirements listed in the following table\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html)

### NICE DCV Client Requirements<a name="what-is-dcv-requirements-client"></a>

The following table lists the minimum system requirements for the NICE DCV clients\.


|  | Native Windows client | Web browser client | Linux client | 
| --- | --- | --- | --- | 
| **Software** |  The Native Windows client is supported on 32\-bit and 64\-bit versions of the following operating systems: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html) The client also requires the following additional software: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html)  |  The web browser client is supported on the following browsers across all desktop operating systems: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html) The web browser client also requires WebGL and asm\.js\. The web browser client is not supported on mobile operating systems, such as Android and iOS\.  |  The Linux client is supported on the following modern Linux operating systems: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/dcv/latest/adminguide/what-is-dcv.html)  | 
| **Network** | The client must be able to connect to the NICE DCV server, and it must be able to communicate over the required port \(8443 by default\)\. | 

## NICE DCV Pricing<a name="what-is-dcv-pricing"></a>

There is no additional charge for using the NICE DCV server on an Amazon EC2 instance\. You pay the standard rates for the instance and other Amazon EC2 features that you use\.

A license is required to install the NICE DCV server on an on\-premises or alternative cloud\-based server\. For more information, see [Licensing the NICE DCV Server](setting-up-license.md)\.