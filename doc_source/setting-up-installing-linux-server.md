# Install the NICE DCV Server on Linux<a name="setting-up-installing-linux-server"></a>

The NICE DCV server is installed using a series of RPM or \.deb packages, depending on your host server's operating system\. The packages install all required packages and their dependencies, and perform the required server configuration\.

**Note**  
You must be signed in as the root user to install the NICE DCV server\.

## Install the NICE DCV Server<a name="linux-server-install"></a>

------
#### [ RHEL/CentOS 6\.x ]

The NICE DCV server is available for RHEL and CentOS 6\.x servers based on the 64\-bit x86 architecture only\.

**To install the NICE DCV server on a RHEL 6\.x and CentOS 6\.x**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. The NICE DCV server packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. To do so, open a terminal window and import the NICE GPG key\.

   ```
   $ sudo rpm --import https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
   ```

1. Download the packages from the [NICE website](http://download.nice-dcv.com)\. The RPM and deb packages are packaged into a `.tgz` archive\. Ensure that you download the correct archive for your operating system\.

   ```
   $ wget https://d1uj6qtbmh3dt5.cloudfront.net/2020.1/Servers/nice-dcv-2020.1-8942-el6-x86_64.tgz
   ```

1. Extract the contents of the `.tgz` archive\.

   ```
   $ tar -xvzf nice-dcv-2020.1-8942-el6-x86_64.tgz
   ```

1. Navigate into the extracted folder\.

   ```
   $ cd nice-dcv-2020.1-8942-el6-x86_64
   ```

1. Install the NICE DCV server\.

   ```
   $ sudo yum install nice-dcv-server-2020.1.8942-1.el6.x86_64.rpm
   ```

1. \(Optional\) If you plan to use virtual sessions, install the `nice-xdcv` package\.

   ```
   $ sudo yum install nice-xdcv-2020.1.338-1.el6.x86_64.rpm
   ```

1. \(Optional\) If you plan to use GPU sharing, install the `nice-dcv-gl` package\. 

   ```
   $ sudo yum install nice-dcv-gl-2020.1.840-1.el6.x86_64.rpm
   ```
**Note**  
You can optionally install the `nice-dcv-gltest` package\. This package includes a simple OpenGL application that can be used to determine whether your virtual sessions are properly configured to use hardware\-based OpenGL\.

1. \(Optional\) If you plan to use NICE DCV with NICE EnginFrame, install the `nice-dcv-simple-external-authenticator` package\. 

   ```
   $ sudo yum install nice-dcv-simple-external-authenticator-2020.1.111-1.el6.x86_64.rpm
   ```

1. \(Optional\) If you plan to support specialized USB devices using USB remotization, install the DCV USB drivers\. 

   To install the DCV USB drivers, you must have Dynamic Kernel Module Support \(DKMS\) installed on your server\. Use the following commands to install DKMS\.

   DKMS can be installed from the Extra Packages for Enterprise Linux \(EPEL\) repository\. Run the following command to enable the EPEL repository:

   ```
   $ sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
   ```

   After you have enabled the EPEL repository, run the following command to install DKMS:

   ```
   $ sudo yum install dkms
   ```

   After you have installed DKMS, run the following command to install the DCV USB drivers:

   ```
   $ sudo dcvusbdriverinstaller
   ```

------
#### [ Amazon Linux 2 and RHEL/CentOS 7\.x ]

The NICE DCV server is available for Amazon Linux 2, RHEL, and CentOS 7\.x servers based on the 64\-bit x86 and 64\-bit ARM architectures\.

**Important**  
The `nice-dcv-gl` and `nice-dcv-gltest` packages aren't available for servers based on the 64\-bit ARM architecture\.

**Note**  
The following instructions are for installing the NICE DCV server on an Amazon Linux 2 RHEL, or CentOS 7\.x server based on the 64\-bit x86 architecture\. To install the NICE DCV server on an Amazon Linux 2, RHEL, or CentOS 7\.x server based on the 64\-bit ARM architecture, replace *x86\_64* with `aarch64` in the following commands\.

**To install the NICE DCV server on Amazon Linux 2, RHEL 7\.x, and CentOS 7\.x**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. The NICE DCV server packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. To do so, open a terminal window and import the NICE GPG key\.

   ```
   $ sudo rpm --import https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
   ```

1. Download the packages from the [NICE website](http://download.nice-dcv.com)\. The RPM and deb packages are packaged into a `.tgz` archive\. Ensure that you download the correct archive for your operating system\.

   ```
   $ wget https://d1uj6qtbmh3dt5.cloudfront.net/2020.1/Servers/nice-dcv-2020.1-8942-el7-x86_64.tgz
   ```

1. Extract the contents of the `.tgz` archive\.

   ```
   $ tar -xvzf nice-dcv-2020.1-8942-el7-x86_64.tgz
   ```

1. Navigate into the extracted folder\.

   ```
   $ cd nice-dcv-2020.1-8942-el7-x86_64
   ```

1. Install the NICE DCV server\.

   ```
   $ sudo yum install nice-dcv-server-2020.1.8942-1.el7.x86_64.rpm
   ```

1. \(Optional\) If you plan to use virtual sessions, install the `nice-xdcv` package\.

   ```
   $ sudo yum install nice-xdcv-2020.1.338-1.el7.x86_64.rpm
   ```

1. \(Optional\) If you plan to use GPU sharing, install the `nice-dcv-gl` package\. 

   ```
   $ sudo yum install nice-dcv-gl-2020.1.840-1.el7.x86_64.rpm
   ```
**Note**  
You can optionally install the `nice-dcv-gltest` package\. This package includes a simple OpenGL application that can be used to determine whether your virtual sessions are properly configured to use hardware\-based OpenGL\.

1. \(Optional\) If you plan to use NICE DCV with NICE EnginFrame, install the `nice-dcv-simple-external-authenticator` package\.

   ```
   $ sudo yum install nice-dcv-simple-external-authenticator-2020.1.111-1.el7.x86_64.rpm
   ```

1. \(Optional\) If you plan to support specialized USB devices using USB remotization, install the DCV USB drivers\. 

   To install the DCV USB drivers, you must have Dynamic Kernel Module Support \(DKMS\) installed on your server\. Use the following commands to install DKMS\.

   DKMS can be installed from the Extra Packages for Enterprise Linux \(EPEL\) repository\. Run the following command to enable the EPEL repository:

   ```
   $ sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
   ```

   After you have enabled the EPEL repository, run the following command to install DKMS:

   ```
   $ sudo yum install dkms
   ```

   After you have installed DKMS, run the following command to install the DCV USB drivers:

   ```
   $ sudo dcvusbdriverinstaller
   ```

------
#### [ RHEL/CentOS 8\.x ]

The NICE DCV server is available for RHEL and CentOS 8\.x servers based on the 64\-bit x86 and 64\-bit ARM architectures\.

**Important**  
The `nice-dcv-gl` and `nice-dcv-gltest` packages aren't available for servers based on the 64\-bit ARM architecture\.

**Note**  
The following instructions are for installing the NICE DCV server on a RHEL or CentOS 8\.x server based on the 64\-bit x86 architecture\. To install the NICE DCV server on a RHEL or CentOS 8\.x server based on the 64\-bit ARM architecture, replace *x86\_64* with `aarch64` in the following commands\.

**To install the NICE DCV server on RHEL 8\.x or CentOS 8\.x**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. The NICE DCV server packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. To do so, open a terminal window and import the NICE GPG key\.

   ```
   $ sudo rpm --import https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
   ```

1. Download the packages from the [NICE website](http://download.nice-dcv.com)\. The RPM and deb packages are packaged into a `.tgz` archive\. Ensure that you download the correct archive for your operating system\.

   ```
   $ wget https://d1uj6qtbmh3dt5.cloudfront.net/2020.1/Servers/nice-dcv-2020.1-8942-el8-x86_64.tgz
   ```

1. Extract the contents of the `.tgz` archive\.

   ```
   $ tar -xvzf nice-dcv-2020.1-8942-el8-x86_64.tgz
   ```

1. Navigate into the extracted folder\.

   ```
   $ cd nice-dcv-2020.1-8942-el8-x86_64
   ```

1. Install the NICE DCV server\.

   ```
   $ sudo yum install nice-dcv-server-2020.1.8942-1.el8.x86_64.rpm
   ```

1. \(Optional\) If you plan to use virtual sessions, install the `nice-xdcv` package\.

   ```
   $ sudo yum install nice-xdcv-2020.1.338-1.el8.x86_64.rpm
   ```

1. \(Optional\) If you plan to use GPU sharing, install the `nice-dcv-gl` package\. 

   ```
   $ sudo yum install nice-dcv-gl-2020.1.840-1.el8.x86_64.rpm
   ```
**Note**  
You can optionally install the `nice-dcv-gltest` package\. This package includes a simple OpenGL application that can be used to determine whether your virtual sessions are properly configured to use hardware\-based OpenGL\.

1. \(Optional\) If you plan to use NICE DCV with NICE EnginFrame, install the `nice-dcv-simple-external-authenticator` package\.

   ```
   $ sudo yum install nice-dcv-simple-external-authenticator-2020.1.111-1.el8.x86_64.rpm
   ```

1. \(Optional\) If you plan to support specialized USB devices using USB remotization, install the DCV USB drivers\. 

   To install the DCV USB drivers, you must have Dynamic Kernel Module Support \(DKMS\) installed on your server\. Use the following commands to install DKMS\.

   DKMS can be installed from the Extra Packages for Enterprise Linux \(EPEL\) repository\. Run the following command to enable the EPEL repository:

   ```
   $ sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
   ```

   After you have enabled the EPEL repository, run the following command to install DKMS:

   ```
   $ sudo yum install dkms
   ```

   After you have installed DKMS, run the following command to install the DCV USB drivers:

   ```
   $ sudo dcvusbdriverinstaller
   ```

------
#### [ SLES 12\.x ]

The NICE DCV server is available for SUSE Linux Enterprise Server \(SLES\) 12\.x servers based on the 64\-bit x86 architecture only\.

**To install the NICE DCV server on SLES 12\.x**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. The NICE DCV server packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. To do so, open a terminal window and import the NICE GPG key\.

   ```
   $ sudo rpm --import https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
   ```

1. Download the packages from the [NICE website](http://download.nice-dcv.com)\. The RPM and deb packages are packaged into a `.tgz` archive\. Ensure that you download the correct archive for your operating system\.

   ```
   $ curl -O https://d1uj6qtbmh3dt5.cloudfront.net/2020.1/Servers/nice-dcv-2020.1-8942-sles12-x86_64.tgz
   ```

1. Extract the contents of the `.tgz` archive\.

   ```
   $ tar -xvzf nice-dcv-2020.1-8942-sles12-x86_64.tgz
   ```

1. Navigate into the extracted folder\.

   ```
   $ cd nice-dcv-2020.1-8942-sles12-x86_64
   ```

1. Install the NICE DCV server\.

   ```
   $ sudo zypper install nice-dcv-server-2020.1.8942-1.sles12.x86_64.rpm
   ```

1. \(Optional\) If you plan to use virtual sessions, install the `nice-xdcv` package\.

   ```
   $ sudo zypper install nice-xdcv-2020.1.338-1.sles12.x86_64.rpm
   ```

1. \(Optional\) If you plan to use GPU sharing, install the `nice-dcv-gl` package\. 

   ```
   $ sudo zypper install nice-dcv-gl-2020.1.840-1.sles12.x86_64.rpm
   ```
**Note**  
You can optionally install the `nice-dcv-gltest` package\. This package includes a simple OpenGL application that can be used to determine whether your virtual sessions are properly configured to use hardware\-based OpenGL\.

1. \(Optional\) If you plan to use NICE DCV with NICE EnginFrame, install the `nice-dcv-simple-external-authenticator` package\. 

   ```
   $ sudo zypper install nice-dcv-simple-external-authenticator-2020.1.111-1.sles12.x86_64.rpm
   ```

1. \(Optional\) If you plan to support specialized USB devices using USB remotization, install the DCV USB drivers\. 

   To install the DCV USB drivers, you must have Dynamic Kernel Module Support \(DKMS\) installed on your server\. Use the following commands to install DKMS\.

   Run the following command to install DKMS:

   ```
   $ sudo zypper install http://download.opensuse.org/repositories/home:/Ximi1970:/Dkms:/Staging/SLE_12_SP4/noarch/dkms-2.5-11.1.noarch.rpm
   ```

   After you have installed DKMS, run the following command to install the DCV USB drivers:

   ```
   $ sudo dcvusbdriverinstaller
   ```

------
#### [ Ubuntu 18\.04 ]

The NICE DCV server is available for Ubuntu servers based on the 64\-bit x86 and 64\-bit ARM architectures\.

**Important**  
The `nice-dcv-gl` and `nice-dcv-gltest` packages aren't available for servers based on the 64\-bit ARM architecture\.

**Note**  
The following instructions are for installing the NICE DCV server on an Ubuntu server based on the 64\-bit x86 architecture\. To install the NICE DCV server on an Ubuntu server based on the 64\-bit ARM architecture, replace *x86\_64* with `arm64` in the following commands\.

**To install the NICE DCV server on Ubuntu 18\.04**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. The NICE DCV server packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. To do so, open a terminal window and import the NICE GPG key\.

   ```
   $ wget https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
   ```

   ```
   $ gpg --import NICE-GPG-KEY
   ```

1. Download the packages from the [NICE website](http://download.nice-dcv.com)\. The RPM and deb packages are packaged into a `.tgz` archive\. Ensure that you download the correct archive for your operating system\.

   ```
   $ wget https://d1uj6qtbmh3dt5.cloudfront.net/2020.1/Servers/nice-dcv-2020.1-8942-ubuntu1804-x86_64.tgz
   ```

1. Extract the contents of the `.tgz` archive\.

   ```
   $ tar -xvzf nice-dcv-2020.1-8942-ubuntu1804-x86_64.tgz
   ```

1. Navigate into the extracted folder\.

   ```
   $ cd nice-dcv-2020.1-8942-ubuntu1804-x86_64
   ```

1. Install the NICE DCV server\.

   ```
   $ sudo apt install ./nice-dcv-server_2020.1.8942-1_amd64.ubuntu1804.deb
   ```

1. \(Optional\) If you plan to use virtual sessions, install the `nice-xdcv` package\.

   ```
   $ sudo apt install ./nice-xdcv_2020.1.338-1_amd64.ubuntu1804.deb
   ```

1. \(Optional\) If you plan to use GPU sharing, install the `nice-dcv-gl` package\. 

   ```
   $ sudo apt install ./nice-dcv-gl_2020.1.840-1_amd64.ubuntu1804.deb
   ```
**Note**  
You can optionally install the `nice-dcv-gltest` package\. This package includes a simple OpenGL application that can be used to determine whether your virtual sessions are properly configured to use hardware\-based OpenGL\.

1. \(Optional\) If you plan to use NICE DCV with NICE EnginFrame, install the `nice-dcv-simple-external-authenticator` package\. 

   ```
   $ sudo apt install ./nice-dcv-simple-external-authenticator_2020.1.111-1_amd64.ubuntu1804.deb
   ```

1. \(Optional\) If you plan to support specialized USB devices using USB remotization, install the DCV USB drivers\. 

   To install the DCV USB drivers, you must have Dynamic Kernel Module Support \(DKMS\) installed on your server\. Use the following commands to install DKMS\.

   DKMS is available in the official Ubuntu repository\. Run the following command to install DKMS:

   ```
   $ sudo apt install dkms
   ```

   After you have installed DKMS, run the following command to install the DCV USB drivers:

   ```
   $ sudo dcvusbdriverinstaller
   ```

------