# Prerequisites for Linux NICE DCV Servers<a name="setting-up-installing-linux-prereq"></a>

NICE DCV enables clients to access a remote graphical X session on a Linux server, which provides access to the corresponding Linux desktop\. NICE DCV supports two types of Linux desktop streaming: console sessions and virtual sessions\. For more information about console and virtual sessions, see [Managing NICE DCV Sessions](managing-sessions.md)\.

This topic explains how to install the prerequisites required to use NICE DCV on a Linux server\.

**Topics**
+ [Install a Desktop Environment and Desktop Manager](#linux-prereq-gui)
+ [Configure the X Server](#linux-prereq-xserver)
+ [Install the glxinfo Utility](#linux-prereq-tools)
+ [Verify OpenGL Software Rendering](#linux-prereq-opengl)
+ [Install and Configure NVIDIA Drivers](#linux-prereq-nvidia)

## Install a Desktop Environment and Desktop Manager<a name="linux-prereq-gui"></a>

To help improve your experience with NICE DCV on a Linux server, you can install a desktop environment and desktop manager\.

A desktop environment is a graphical user interface \(GUI\) that helps you to interact with the Linux operating system\. There are several desktop environments, and NICE DCV works with many of them\. A desktop manager is a program that manages the user login screen, and starts and stops the desktop environment sessions and the X server\.

The following tabbed content shows the steps for installing the default desktop environment and desktop manager on the supported operating systems\.

------
#### [ RHEL 7\.x ]

The default desktop environment for RHEL 7\.x is Gnome3 and the default desktop manager is GDM\.

**To install and configure the desktop environment and desktop manager on RHEL 7\.x**

1. Install the desktop environment and the desktop manager packages\.

   ```
   $ sudo yum groupinstall 'Server with GUI'
   ```

1. Update the software packages to ensure that the Linux server is up to date\.

   ```
   $ sudo yum upgrade
   ```

1. Reboot the Linux server\.

   ```
   $ sudo reboot
   ```

------
#### [ CentOS 7\.x ]

The default desktop environment for CentOS 7\.x is Gnome3 and the default desktop manager is GDM\.

**To install and configure the desktop environment and desktop manager on CentOS 7\.x**

1. Install the desktop environment and the desktop manager packages\.

   ```
   $ sudo yum groupinstall "GNOME Desktop"
   ```

1. Update the software packages to ensure that the Linux server is up to date\.

   ```
   $ sudo yum upgrade
   ```

1. Reboot the Linux server\.

   ```
   $ sudo reboot
   ```

------
#### [ RHEL 6\.x and CentOS 6\.x ]

The default desktop environment for RHEL 6\.x and CentOS 6\.x is Gnome and the default desktop manager is GDM\.

**To install and configure the desktop environment and desktop manager on RHEL 6\.x and CentOS 6\.x**

1. Install the desktop environment and the desktop manager packages\.

   ```
   $ sudo yum groupinstall\"X Window System" "Desktop" "General Purpose Desktop"
   ```

1. Update the software packages to ensure that the Linux server is up to date\.

   ```
   $ sudo yum upgrade
   ```

1. Reboot the Linux server\.

   ```
   $ sudo reboot
   ```

------
#### [ Amazon Linux 2 ]

The default desktop environment for Amazon Linux 2 is Gnome3 and the default desktop manager is GDM\.

**To install and configure the desktop environment and desktop manager on Amazon Linux 2**

1. Install the desktop environment and the desktop manager packages\.

   ```
   $ sudo yum install gdm gnome-session gnome-classic-session gnome-session-xsession
   ```

   ```
   $ sudo yum install xorg-x11-server-Xorg xorg-x11-fonts-Type1 xorg-x11-drivers 
   ```

   ```
   $ sudo yum install gnome-terminal gnu-free-fonts-common gnu-free-mono-fonts gnu-free-sans-fonts gnu-free-serif-fonts
   ```

1. Update the software packages to ensure that the Linux server is up to date\.

   ```
   $ sudo yum upgrade
   ```

1. Reboot the Linux server\.

   ```
   $ sudo reboot
   ```

------
#### [ Ubuntu 18\.x ]

The default desktop environment for Ubuntu 18\.x is Gnome3 and the default desktop manager is GDM3\. GDM3 is currently not supported with NICE DCV console sessions\. We recommend that you use the LightDM desktop manager if you plan to work with NICE DCV console sessions\.

**To install and configure the desktop environment and desktop manager on Ubuntu 18\.x**

1. Install the desktop environment and the desktop manager packages\.

   ```
   $ sudo apt update
   ```

   ```
   $ sudo apt install ubuntu-desktop
   ```

   Install LightDM\.

   ```
   $ sudo apt install lightdm
   ```

1. Update the software packages to ensure that the Linux server is up to date\.

   ```
   $ sudo apt upgrade
   ```

1. Reboot the Linux server\.

   ```
   $ sudo reboot
   ```

------
#### [ SUSE Linux Enterprise 12\.x ]

The default desktop environment for SUSE Linux Enterprise 12\.x is SLE Classic and the default desktop manager is GDM\.

**To install and configure the desktop environment and desktop manager on SUSE Linux Enterprise 12\.x**

1. Install the desktop environment and the desktop manager packages\.

   ```
   $ sudo zypper install -t pattern gnome-basic
   ```

   ```
   $ sudo sed -i "s/DISPLAYMANAGER=\"\"/DISPLAYMANAGER=\"gdm\"/" /etc/sysconfig/displaymanager
   ```

   ```
   $ sudo sed -i "s/DEFAULT_WM=\"\"/DEFAULT_WM=\"sle-classic\"/" /etc/sysconfig/windowmanager
   ```

1. Update the software packages to ensure that the Linux server is up to date\.

   ```
   $ sudo zypper update
   ```

1. Reboot the Linux server\.

   ```
   $ sudo reboot
   ```

------

## Configure the X Server<a name="linux-prereq-xserver"></a>

If you intend to use a console session or GPU sharing, you must ensure that your Linux server has a properly configured and running X server\.

**Note**  
If you intend to use virtual sessions without GPU sharing, you do not need an X server\.

The X server packages are typically installed as dependencies of the desktop environment and the desktop manager\. We recommend that you configure the X server to start automatically when your Linux server boots\.

The following tabbed content shows how to configure and start the X server on the supported operating systems\.

------
#### [ RHEL 6\.x and CentOS 6\.x ]

**To configure and start the X server on RHEL 6\.x and CentOS 6\.x**

1. Configure the X server to start automatically when the Linux server boots\.

   ```
   $ cat /etc/inittab  | grep "id.*initdefault"
   ```

   If the command returns `id:5:initdefault`, the X server is already configured to start automatically\. Continue to the next step\.

   If the command returns `id:3:initdefault`, the X server is not configured to start automatically\. Run the following command\.

   ```
   $ sudo sed -i "s/id:3:initdefault:/id:5:initdefault:/" /etc/inittab
   ```

1. Start the X server\.

   ```
   $ sudo init 5
   ```

1. Verify that the X server is running\.

   ```
   $ ps aux | grep X | grep -v grep
   ```

   The following shows example output if the X server is running\.

   ```
   root      1891  0.0  0.7 277528 30448 tty7     Ssl+ 10:59   0:00 /usr/bin/Xorg :0 -background none -verbose -auth /run/gdm/auth-for-gdm-wltseN/database -seat seat0 vt7
   ```

------
#### [ RHEL 7\.x, CentOS 7\.x, Amazon Linux 2, Ubuntu 18\.x, and SUSE Linux Enterprise 12\.x ]

**To configure and start the X server on RHEL 7\.x, CentOS 7\.x, Amazon Linux 2, Ubuntu 18\.x, and SUSE Linux Enterprise 12\.x**

1. Configure the X server to start automatically when the Linux server boots\.

   ```
   $ sudo systemctl get-default
   ```

   If the command returns `graphical.target`, the X server is already configured to start automatically\. Continue to the next step\.

   If the command returns `multi-user.target`, the X server is not configured to start automatically\. Run the following command:

   ```
   $ sudo systemctl set-default graphical.target
   ```

1. Start the X server\.

   ```
   $ sudo systemctl isolate graphical.target
   ```

1. Verify that the X server is running\.

   ```
   $ ps aux | grep X | grep -v grep
   ```

   The following shows example output if the X server is running\.

   ```
   root      1891  0.0  0.7 277528 30448 tty7     Ssl+ 10:59   0:00 /usr/bin/Xorg :0 -background none -verbose -auth /run/gdm/auth-for-gdm-wltseN/database -seat seat0 vt7
   ```

------

## Install the glxinfo Utility<a name="linux-prereq-tools"></a>

The glxinfo utility provides information about your Linux server's OpenGL configuration\. It can be used to determine whether your Linux server is configured to support OpenGL hardware or software rendering, and it provides information about the drivers and supported extensions\.

The glxinfo utility is installed as a package dependency of DCV GL\. Therefore, if you installed DCV GL, the glxinfo utility is already installed on your Linux server\.

**To install the glxinfo utility**  
Run the following command:
+ RHEL 6\.x/7\.x, CentOs 6\.x/7\.x, and Amazon Linux 2

  ```
  $ sudo yum install glx-utils
  ```
+ Ubuntu 18\.x

  ```
  $ sudo apt install mesa-utils
  ```
+ SUSE Linux Enterprise 12\.x

  ```
  $ sudo zypper in Mesa-demo-x
  ```

## Verify OpenGL Software Rendering<a name="linux-prereq-opengl"></a>

On non\-GPU Linux servers, OpenGL is only supported in software rendering mode using the Mesa drivers\. If you're using a non\-GPU Linux server, and you intend to use OpenGL, ensure that the Mesa drivers are installed and properly configured on your Linux server\.

**Note**  
This applies to non\-GPU Linux servers only\.

**To verify that OpenGL software rendering is available**  
Make sure that the X server is running, and use the following command:

```
$ sudo DISPLAY=:0 XAUTHORITY=$(ps aux | grep "X.*\-auth" | grep -v grep | sed -n 's/.*-auth \([^ ]\+\).*/\1/p') glxinfo | grep -i "opengl.*version"
```

The following shows example output if OpenGL software rendering is available:

```
OpenGL core profile version string: 3.3 (Core Profile) Mesa 17.0.5
OpenGL core profile shading language version string: 3.30
OpenGL version string: 3.0 Mesa 17.0.5
OpenGL shading language version string: 1.30
OpenGL ES profile version string: OpenGL ES 3.0 Mesa 17.0.5
OpenGL ES profile shading language version string: OpenGL ES GLSL ES 3.00
```

## Install and Configure NVIDIA Drivers<a name="linux-prereq-nvidia"></a>

With Linux servers that have a dedicated NVIDIA GPU, you must ensure that the appropriate NVIDIA drivers are installed and properly configured\. For more information about installing the NVIDIA drivers on an Amazon EC2 Linux instance, see [Installing the NVIDIA Driver on Linux Servers](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-nvidia-driver.html) in the *Amazon EC2 User Guide for Linux Instances*\.

**Note**  
This applies to Linux servers with NVIDIA GPUs only\.
The GRID drivers support up to four 4K displays per GPU, while the gaming drivers support a single 4K display per GPU\.

After you have installed the NVIDIA drivers on your Linux server, you must update the `xorg.conf`\.

**To generate an updated xorg\.conf**

1. Run the following command\.

   ```
   nvidia-xconfig --preserve-busid --enable-all-gpus
   ```

   If you are using a G3 or G4 Amazon EC2 instance and you want to use a multi\-monitor console session, include the `--connected-monitor=DFP-0,DFP-1,DFP-2,DFP-3` parameter as follows\.

   ```
   nvidia-xconfig --preserve-busid --enable-all-gpus --connected-monitor=DFP-0,DFP-1,DFP-2,DFP-3
   ```
**Note**  
Make sure that your server does not have the legacy `/etc/X11/XF86Config` file\. If it does, `nvidia-xconfig` updates that configuration file instead of generating the required `/etc/X11/xorg.conf` file\. Run the following command to remove the legacy `XF86Config` file:  

   ```
   rm -rf /etc/X11/XF86Config*
   ```

1. Restart the X server for the changes to take effect\.
   + RHEL 7\.x, CentOs 7\.x, Amazon Linux 2, Ubuntu 18\.x, and SUSE Linux Enterprise 12\.x

     ```
     $ sudo systemctl isolate multi-user.target
     ```

     ```
     $ sudo systemctl isolate graphical.target
     ```
   + RHEL 6\.x and CentOs 6\.x

     ```
     $ sudo init 3
     ```

     ```
     $ sudo init 5
     ```

You must also ensure that OpenGL hardware rendering is available on the Linux server\.

**To verify that OpenGL hardware rendering is available**  
Use the following command to ensure that the X server is running\.

```
$ sudo DISPLAY=:0 XAUTHORITY=$(ps aux | grep "X.*\-auth" | grep -v grep | sed -n 's/.*-auth \([^ ]\+\).*/\1/p') glxinfo | grep -i "opengl.*version"
```

The following shows example output if OpenGL hardware rendering is available\.

```
OpenGL core profile version string: 4.4.0 NVIDIA 390.75
OpenGL core profile shading language version string: 4.40 NVIDIA via Cg compiler
OpenGL version string: 4.6.0 NVIDIA 390.75
OpenGL shading language version string: 4.60 NVIDIA
OpenGL ES profile version string: OpenGL ES 3.2 NVIDIA 390.75
OpenGL ES profile shading language version string: OpenGL ES GLSL ES 3.20
```