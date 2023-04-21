# Prerequisites for Linux NICE DCV servers<a name="setting-up-installing-linux-prereq"></a>

NICE DCV enables clients to access a remote graphical X session on a Linux server\. This provides access to the corresponding Linux desktop\. NICE DCV supports two types of Linux desktop streaming: console sessions and virtual sessions\. For more information about console and virtual sessions, see [Managing NICE DCV sessions](managing-sessions.md)\.

This topic describes how to install the prerequisites required to use NICE DCV on a Linux server\.

**Topics**
+ [Install a desktop environment and desktop manager](#linux-prereq-gui)
+ [Disable the Wayland protocol \(GDM3 only\)](#linux-prereq-wayland)
+ [Configure the X Server](#linux-prereq-xserver)
+ [Install the glxinfo utility](#linux-prereq-tools)
+ [Verify OpenGL software rendering](#linux-prereq-opengl)
+ [Install GPU drivers for graphics instances](#linux-prereq-gpu)
+ [Install XDummy driver for non\-GPU instances](#linux-prereq-nongpu)

## Install a desktop environment and desktop manager<a name="linux-prereq-gui"></a>

Install a desktop environment and desktop manager to improve your experience with NICE DCV on a Linux server\.

A desktop environment is a graphical user interface \(GUI\) that helps you to interact with the Linux operating system\. There are several desktop environments, and NICE DCV works with many of them\. A desktop manager is a program that manages the user login screen, and starts and stops the desktop environment sessions and the X server\.

The following tabbed content shows the steps for installing the default desktop environment and desktop manager on the supported operating systems and also shows how to configure and start the X server on the supported operating systems\.

------
#### [ RHEL, CentOS, and Rocky Linux ]

The default desktop environment for RHEL, CentOS , and Rocky Linux is Gnome3 and the default desktop manager is GDM\.

**To install and configure the desktop environment and desktop manager on RHEL, CentOS, and Rocky Linux**

1. Install the desktop environment and the desktop manager packages\.
   + RHEL, CentOS, and Rocky Linux and above

     ```
     $ sudo yum groupinstall 'Server with GUI'
     ```
   + CentOS

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

For Ubuntu 18\.x, the default desktop environment is Gnome3 and the default desktop manager is GDM3\. With Ubuntu 18\.x, GDM3 isn't currently supported with NICE DCV console sessions\. For this reason, we recommend that you use the LightDM desktop manager if you plan to work with NICE DCV console sessions\.

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
#### [ Ubuntu 20\.x and 22\.x ]

For Ubuntu 20\.x/22\.x, the default desktop environment is Gnome3 and the default desktop manager is GDM3\. Starting with Ubuntu 20\.x, LightDM isn't supported anymore with NICE DCV\.

**To install and configure the desktop environment and desktop manager on Ubuntu 20\.x/22\.x**

1. Install the desktop environment and the desktop manager packages\.

   ```
   $ sudo apt update
   ```

   ```
   $ sudo apt install ubuntu-desktop
   ```

   Install GDM3

   ```
   $ sudo apt install gdm3
   ```

1. Verify that GDM3 is set as the default desktop manager\.

   ```
   $ cat /etc/X11/default-display-manager
   ```

   The output is as follows\.

   ```
   /usr/sbin/gdm3
   ```

   If GDM3 isn't set as the default desktop manager, use the following command to set it as the default\.

   ```
   $ sudo dpkg-reconfigure gdm3
   ```

1. Update the software packages to ensure that the Linux server is up to date\.

   ```
   $ sudo apt upgrade
   ```

1. Reboot the Linux server\.

   ```
   $ sudo reboot
   ```

**Note**  
When using a version of NICE DCV older than 2022\.2 with **Virtual Sessions**, you may run into [a known GDM issue](https://gitlab.gnome.org/GNOME/gdm/-/issues/650)\. To make virtual sessions work correctly, you can adopt one of the following solutions:  
**On servers that do not have a GPU**, you can disable the desktop manager because it's not required to run virtual sessions\. Configure the system to run in multi\-user mode by running the following command before creating virtual sessions:  

  ```
  sudo systemctl isolate multi-user.target
  ```
**On servers with a GPU**, in addition to disabling the desktop manager, you need to start an X server on the system before creating virtual sessions\. To do this, run the following commands:  

  ```
  sudo systemctl isolate multi-user.target
  ```

  ```
  sudo dcvstartx &
  ```
NICE DCV 2022\.2 and newer are not affected by this issue\.

------
#### [ SUSE Linux Enterprise 12\.x ]

The default desktop environment for SUSE Linux Enterprise 12\.x is SLE Classic and the default desktop manager is GDM\.

**To install and configure the desktop environment and desktop manager on SUSE Linux Enterprise 12\.x**

1. Install the desktop environment and the desktop manager packages\.

   ```
   $ sudo zypper install -t pattern gnome_basic
   ```

1. Verify that GDM is set as the default desktop manager\.

   ```
   $ sudo update-alternatives --set default-displaymanager /usr/lib/X11/displaymanagers/gdm
   ```

   ```
   $ sudo sed -i "s/DEFAULT_WM=\"\"/DEFAULT_WM=\"gnome\"/" /etc/sysconfig/windowmanager
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
#### [ SUSE Linux Enterprise 15\.x ]

The default desktop environment for SUSE Linux Enterprise 15\.x is SLE Classic and the default desktop manager is GDM3\.

**To install and configure the desktop environment and desktop manager on SUSE Linux Enterprise 15\.x**

1. Install the desktop environment and the desktop manager packages\.

   ```
   $ sudo zypper install -t pattern gnome_basic
   ```

1. Verify that GDM is set as the default desktop manager\.

   ```
   $ sudo update-alternatives --set default-displaymanager /usr/lib/X11/displaymanagers/gdm
   ```

   ```
   $ sudo sed -i "s/DEFAULT_WM=\"\"/DEFAULT_WM=\"gnome\"/" /etc/sysconfig/windowmanager
   ```

1. Update the software packages to ensure that the Linux server is up to date\.

   ```
   $ sudo zypper update
   ```

1. Reboot the Linux server\.

   ```
   $ sudo reboot
   ```

**Note**  
When using a version of NICE DCV older than 2022\.2 with **Virtual Sessions**, you may run into [a known GDM issue](https://gitlab.gnome.org/GNOME/gdm/-/issues/650)\. To make virtual sessions work correctly, you can adopt one of the following solutions:  
**On servers that do not have a GPU**, you can disable the desktop manager because it's not required to run virtual sessions\. Configure the system to run in multi\-user mode by running the following command before creating virtual sessions:  

  ```
  sudo systemctl isolate multi-user.target
  ```
**On servers with a GPU**, in addition to disabling the desktop manager, you need to start an X server on the system before creating virtual sessions\. To do this, run the following commands:  

  ```
  sudo systemctl isolate multi-user.target
  ```

  ```
  sudo dcvstartx &
  ```
NICE DCV 2022\.2 and newer are not affected by this issue\.

------

## Disable the Wayland protocol \(GDM3 only\)<a name="linux-prereq-wayland"></a>

NICE DCV doesn't support the Wayland protocol\. If you're using the GDM3 desktop manager, you must disable the Wayland protocol\. If you aren't using GDM3, skip this step\.

**To disable the Wayland protocol**

1. Open the following file using your preferred text editor\.
   + RHEL, CentOS, and SUSE Linux Enterprise 15\.x

     ```
     /etc/gdm/custom.conf
     ```
   + Ubuntu 18\.x/20\.x/22\.x

     ```
     /etc/gdm3/custom.conf
     ```

1. In the `[daemon]` section, set `WaylandEnable` to `false`\.

   ```
   [daemon]
   WaylandEnable=false
   ```

1. Restart the GDM service\.
   + RHEL and CentOS

     ```
     $ sudo systemctl restart gdm
     ```
   + Ubuntu 18\.x/20\.x/22\.x

     ```
     $ sudo systemctl restart gdm3
     ```
   + SUSE Linux Enterprise 15\.x

     ```
     $ sudo systemctl restart xdm
     ```

## Configure the X Server<a name="linux-prereq-xserver"></a>

If you intend to use a console session or GPU sharing, you must ensure that your Linux server has a properly configured and running X server\.

**Note**  
If you intend to use virtual sessions without GPU sharing, you don't need an X server\.

The X server packages are typically installed as dependencies of the desktop environment and the desktop manager\. We recommend that you configure the X server to start automatically when your Linux server boots\.

**To configure and start the X server on RHEL, CentOS, Rocky Linux, Amazon Linux 2, Ubuntu 18\.x, 20\.x, 22\.x, and SUSE Linux Enterprise 12\.x, 15\.x:**

1. Configure the X server to start automatically when the Linux server boots\.

   `$ sudo systemctl get-default`

   If the command returns `graphical.target`, the X server is already configured to start automatically\. Continue to the next step\. 

   If the command returns `multi-user.target`, the X server isn't configured to start automatically\. Execute the following command: 

   `$ sudo systemctl set-default graphical.target`

1. Start the X server\. 

   `$ sudo systemctl isolate graphical.target `

1. Verify that the X server is running\.

   `$ ps aux | grep X | grep -v grep `

   The following shows example output if the X server is running\. 

   `root 1891 0.0 0.7 277528 30448 tty7 Ssl+ 10:59 0:00 /usr/bin/Xorg :0 -background none -verbose -auth /run/gdm/auth-for-gdm-wltseN/database -seat seat0 vt7 `

## Install the glxinfo utility<a name="linux-prereq-tools"></a>

The glxinfo utility provides information about your Linux server's OpenGL configuration\. The utility can be used to determine whether your Linux server is configured to support OpenGL hardware or software rendering\. It provides information about the drivers and supported extensions\.

The glxinfo utility is installed as a package dependency of DCV GL\. Therefore, if you installed DCV GL, the glxinfo utility is already installed on your Linux server\.

------
#### [ RHEL, CentOS, Rocky Linux, and Amazon Linux 2 ]

**To install the glxinfo utility**  
Run the following command:

```
$ sudo yum install glx-utils
```

------
#### [ Ubuntu ]

**To install the glxinfo utility**  
Run the following command:

```
$ sudo apt install mesa-utils
```

------
#### [ SUSE Linux Enterprise ]

**To install the glxinfo utility**  
Run the following command:

```
$ sudo zypper in Mesa-demo-x
```

------

## Verify OpenGL software rendering<a name="linux-prereq-opengl"></a>

On non\-GPU Linux servers, OpenGL is only supported in software rendering mode using the Mesa drivers\. If you're using a non\-GPU Linux server and intend to use OpenGL, ensure that the Mesa drivers are installed and properly configured on your Linux server\.

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

## Install GPU drivers for graphics instances<a name="linux-prereq-gpu"></a>

**Topics**
+ [Install and configure NVIDIA drivers](#gpu-nvidia)
+ [Install and Configure AMD Drivers](#gpu-amd)

### Install and configure NVIDIA drivers<a name="gpu-nvidia"></a>

With Linux servers that have a dedicated NVIDIA GPU, ensure that the appropriate NVIDIA drivers are installed and properly configured\. For instructions on how to install the NVIDIA drivers on an Amazon EC2 Linux instance, see [Installing the NVIDIA Driver on Linux Servers](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-nvidia-driver.html) in the *Amazon EC2 User Guide for Linux Instances*\.

**Note**  
This applies to Linux servers with NVIDIA GPUs only\.
The GRID drivers support up to four 4K displays for each GPU installed\. The gaming drivers support only one 4K display for each GPU installed\.

After you installed the NVIDIA drivers on your Linux server, update the `xorg.conf`\.

**To generate an updated xorg\.conf**

1. Run the following command\.

   ```
   sudo nvidia-xconfig --preserve-busid --enable-all-gpus
   ```

   If you're using a G3 or G4 Amazon EC2 instance and you want to use a multi\-monitor console session, include the `--connected-monitor=DFP-0,DFP-1,DFP-2,DFP-3` parameter\. This is as follows\.

   ```
   sudo nvidia-xconfig --preserve-busid --enable-all-gpus --connected-monitor=DFP-0,DFP-1,DFP-2,DFP-3
   ```
**Note**  
Make sure that your server doesn't have the legacy `/etc/X11/XF86Config` file\. If it does, `nvidia-xconfig` updates that configuration file instead of generating the required `/etc/X11/xorg.conf` file\. Run the following command to remove the legacy `XF86Config` file:  

   ```
   sudo rm -rf /etc/X11/XF86Config*
   ```

1. Restart the X server for the changes to take effect\.
   + 

     ```
     $ sudo systemctl isolate multi-user.target
     ```

     ```
     $ sudo systemctl isolate graphical.target
     ```

**To verify that your NVIDIA GPU supports hardware\-based video encoding**  
Make sure that it supports NVENC encoding and that it has compute capabilities greater than or equal to 3\.0, or greater than or equal to 3\.5 for Ubuntu 20\.

To verify NVENC support, see the [ NVIDIA Video Encode and Decode GPU Support Matrix](https://developer.nvidia.com/video-encode-and-decode-gpu-support-matrix-new#Encoder)\. To check the compute capabilities, see the [NVIDIA Compute Capacility tables](https://developer.nvidia.com/cuda-gpus)\. 

If your NVIDIA GPU doesn't support NVENC encoding or if it doesn't have the required compute capabilities, software\-based video encoding is used\.

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

### Install and Configure AMD Drivers<a name="gpu-amd"></a>

An instance with an attached AMD GPU, such as a G4ad instance, must have the appropriate AMD driver installed\. For instructions on how to install the AMD GPU drivers on a compatible Amazon EC2 instance, see [ Install AMD drivers on Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-amd-driver.html)\.

For more information about Amazon EC2 G4ad instances, see the [Deep dive on the new Amazon EC2 G4ad instances ](http://aws.amazon.com/blogs/compute/deep-dive-on-the-new-amazon-ec2-g4ad-instances/) blog post\.

## Install XDummy driver for non\-GPU instances<a name="linux-prereq-nongpu"></a>

**Topics**
+ [Install and configure the XDummy driver](#gpu-xdummy)

### Install and configure the XDummy driver<a name="gpu-xdummy"></a>

To use console sessions on Linux servers that do not have a dedicated GPU, ensure that the Xdummy driver is installed and properly configured\. The XDummy driver allows the X server to run with a virtual framebuffer when no real GPU is present\.

**Note**  
This is not required if you intend to use virtual sessions\.
The XDummy driver is able to support only resolutions defined in its configuration\.

------
#### [ RHEL, CentOS, Rocky Linux, and Amazon Linux 2 ]

**To install the XDummy driver**  
Run the following command:

```
$ sudo yum install xorg-x11-drv-dummy
```

------
#### [ Ubuntu ]

**To install the XDummy driver**  
Run the following command:

```
$ sudo apt install xserver-xorg-video-dummy
```

------
#### [ SUSE Linux Enterprise ]

**To install the XDummy driver**  
Run the following command:

```
$ sudo zypper in xf86-video-dummy
```

------

After you installed the XDummy drivers on your Linux server, update the `xorg.conf`\.

**To configure XDummy in xorg\.conf**

1. Open the `/etc/X11/xorg.conf` file with your preferred text editor\.

1. Add the following sections to the configuration\.

   ```
   Section "Device"
       Identifier "DummyDevice"
       Driver "dummy"
       Option "ConstantDPI" "true"
       Option "IgnoreEDID" "true"
       Option "NoDDC" "true"
       VideoRam 2048000
   EndSection
   
   Section "Monitor"
       Identifier "DummyMonitor"
       HorizSync   5.0 - 1000.0
       VertRefresh 5.0 - 200.0
       Modeline "1920x1080" 23.53 1920 1952 2040 2072 1080 1106 1108 1135
       Modeline "1600x900" 33.92 1600 1632 1760 1792 900 921 924 946
       Modeline "1440x900" 30.66 1440 1472 1584 1616 900 921 924 946
       ModeLine "1366x768" 72.00 1366 1414 1446 1494  768 771 777 803
       Modeline "1280x800" 24.15 1280 1312 1400 1432 800 819 822 841
       Modeline "1024x768" 18.71 1024 1056 1120 1152 768 786 789 807
   EndSection
   
   Section "Screen"
       Identifier "DummyScreen"
       Device "DummyDevice"
       Monitor "DummyMonitor"
       DefaultDepth 24
       SubSection "Display"
           Viewport 0 0
           Depth 24
           Modes "1920x1080" "1600x900" "1440x900" "1366x768" "1280x800" "1024x768"
           virtual 1920 1080
       EndSubSection
   EndSection
   ```
**Note**  
The configuration provided is an example\. You can add more modes, and set a different `virtual` resolution\. You can also configure more than one dummy monitor\.

1. Restart the X server for the changes to take effect\.
   + 

     ```
     $ sudo systemctl isolate multi-user.target
     ```

     ```
     $ sudo systemctl isolate graphical.target
     ```