# Install the NICE DCV Server on Linux<a name="setting-up-installing-linux-server"></a>

The NICE DCV server is installed using a series of RPM or \.deb packages, depending on your host server's operating system\. The packages install all required packages and their dependencies, and perform the required server configuration\.

**Note**  
You must be signed in as the root user to install the NICE DCV server\.

## Install the NICE DCV Server<a name="linux-server-install"></a>

------
#### [ RHEL 6\.x and CentOS 6\.x ]

**To install the NICE DCV server on a RHEL 6\.x and CentOS 6\.x**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. The NICE DCV server packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. To do so, open a terminal window and import the NICE GPG key\.

   ```
   $ sudo rpm --import https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
   ```

1. Download the packages from the [NICE website](http://download.nice-dcv.com)\. The RPM and deb packages are packaged into a `.tgz` archive\. Ensure that you download the correct archive for your operating system\.

   ```
   $ wget https://d1uj6qtbmh3dt5.cloudfront.net/2020.0/Servers/nice-dcv-2020.0-8428-el6.tgz
   ```

1. Extract the contents of the `.tgz` archive\.

   ```
   $ tar -xvzf nice-dcv-2020.0-8428-el6.tgz
   ```

1. Navigate into the extracted folder\.

   ```
   $ cd nice-dcv-2020.0-8428-el6
   ```

1. Install the NICE DCV server\.

   ```
   $ sudo yum install nice-dcv-server-2020.0.8428-1.el6.x86_64.rpm
   ```

1. \(Optional\) If you plan to use virtual sessions, install the `nice-xdcv` package\.

   ```
   $ sudo yum install nice-xdcv-2020.0.296-1.el6.x86_64.rpm
   ```

1. \(Optional\) If you plan to use GPU sharing, install the `nice-dcv-gl` package\. 

   ```
   $ sudo yum install nice-dcv-gl-2020.0.759-1.el6.x86_64.rpm
   ```
**Note**  
You can optionally install the `nice-dcv-gltest` package\. This package includes a simple OpenGL application that can be used to determine whether your virtual sessions are properly configured to use hardware\-based OpenGL\.

1. \(Optional\) If you plan to use NICE DCV with NICE EnginFrame, install the `nice-dcv-simple-external-authenticator` package\. 

   ```
   $ sudo yum install nice-dcv-simple-external-authenticator-2020.0.87-1.el6.x86_64.rpm
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
#### [ Amazon Linux 2, RHEL 7\.x, and CentOS 7\.x ]

**To install the NICE DCV server on Amazon Linux 2, RHEL 7\.x, and CentOS 7\.x**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. The NICE DCV server packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. To do so, open a terminal window and import the NICE GPG key\.

   ```
   $ sudo rpm --import https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
   ```

1. Download the packages from the [NICE website](http://download.nice-dcv.com)\. The RPM and deb packages are packaged into a `.tgz` archive\. Ensure that you download the correct archive for your operating system\.

   ```
   $ wget https://d1uj6qtbmh3dt5.cloudfront.net/2020.0/Servers/nice-dcv-2020.0-8428-el7.tgz
   ```

1. Extract the contents of the `.tgz` archive\.

   ```
   $ tar -xvzf nice-dcv-2020.0-8428-el7.tgz
   ```

1. Navigate into the extracted folder\.

   ```
   $ cd nice-dcv-2020.0-8428-el7
   ```

1. Install the NICE DCV server\.

   ```
   $ sudo yum install nice-dcv-server-2020.0.8428-1.el7.x86_64.rpm
   ```

1. \(Optional\) If you plan to use virtual sessions, install the `nice-xdcv` package\.

   ```
   $ sudo yum install nice-xdcv-2020.0.296-1.el7.x86_64.rpm
   ```

1. \(Optional\) If you plan to use GPU sharing, install the `nice-dcv-gl` package\. 

   ```
   $ sudo yum install nice-dcv-gl-2020.0.759-1.el7.x86_64.rpm
   ```
**Note**  
You can optionally install the `nice-dcv-gltest` package\. This package includes a simple OpenGL application that can be used to determine whether your virtual sessions are properly configured to use hardware\-based OpenGL\.

1. \(Optional\) If you plan to use NICE DCV with NICE EnginFrame, install the `nice-dcv-simple-external-authenticator` package\. 

   ```
   $ sudo yum install nice-dcv-simple-external-authenticator-2020.0.87-1.el7.x86_64.rpm
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
#### [ SUSE Linux Enterprise 12\.x ]

**To install the NICE DCV server on SUSE Linux Enterprise 12\.x**

1. Launch and connect to the server on which to install the NICE DCV server\.

1. The NICE DCV server packages are digitally signed with a secure GPG signature\. To allow the package manager to verify the package signature, you must import the NICE GPG key\. To do so, open a terminal window and import the NICE GPG key\.

   ```
   $ sudo rpm --import https://d1uj6qtbmh3dt5.cloudfront.net/NICE-GPG-KEY
   ```

1. Download the packages from the [NICE website](http://download.nice-dcv.com)\. The RPM and deb packages are packaged into a `.tgz` archive\. Ensure that you download the correct archive for your operating system\.

   ```
   $ curl -O https://d1uj6qtbmh3dt5.cloudfront.net/2020.0/Servers/nice-dcv-2020.0-8428-sles12.tgz
   ```

1. Extract the contents of the `.tgz` archive\.

   ```
   $ tar -xvzf nice-dcv-2020.0-8428-sles12.tgz
   ```

1. Navigate into the extracted folder\.

   ```
   $ cd nice-dcv-2020.0-8428-sles12
   ```

1. Install the NICE DCV server\.

   ```
   $ sudo zypper install nice-dcv-server-2020.0.8428-1.sles12.x86_64.rpm
   ```

1. \(Optional\) If you plan to use virtual sessions, install the `nice-xdcv` package\.

   ```
   $ sudo zypper install nice-xdcv-2020.0.296-1.sles12.x86_64.rpm
   ```

1. \(Optional\) If you plan to use GPU sharing, install the `nice-dcv-gl` package\. 

   ```
   $ sudo zypper install nice-dcv-gl-2020.0.759-1.sles12.x86_64.rpm
   ```
**Note**  
You can optionally install the `nice-dcv-gltest` package\. This package includes a simple OpenGL application that can be used to determine whether your virtual sessions are properly configured to use hardware\-based OpenGL\.

1. \(Optional\) If you plan to use NICE DCV with NICE EnginFrame, install the `nice-dcv-simple-external-authenticator` package\. 

   ```
   $ sudo zypper install nice-dcv-simple-external-authenticator-2020.0.87-1.sles12.x86_64.rpm
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
   $ wget https://d1uj6qtbmh3dt5.cloudfront.net/2020.0/Servers/nice-dcv-2020.0-8428-ubuntu1804.tgz
   ```

1. Extract the contents of the `.tgz` archive\.

   ```
   $ tar -xvzf nice-dcv-2020.0-8428-ubuntu1804.tgz
   ```

1. Navigate into the extracted folder\.

   ```
   $ cd nice-dcv-2020.0-8428-ubuntu1804
   ```

1. Install the NICE DCV server\.

   ```
   $ sudo apt install ./nice-dcv-server_2020.0.8428-1_amd64.ubuntu1804.deb
   ```

1. \(Optional\) If you plan to use virtual sessions, install the `nice-xdcv` package\.

   ```
   $ sudo apt install ./nice-xdcv_2020.0.296-1_amd64.ubuntu1804.deb
   ```

1. \(Optional\) If you plan to use GPU sharing, install the `nice-dcv-gl` package\. 

   ```
   $ sudo apt install ./nice-dcv-gl_2020.0.759-1_amd64.ubuntu1804.deb
   ```
**Note**  
You can optionally install the `nice-dcv-gltest` package\. This package includes a simple OpenGL application that can be used to determine whether your virtual sessions are properly configured to use hardware\-based OpenGL\.

1. \(Optional\) If you plan to use NICE DCV with NICE EnginFrame, install the `nice-dcv-simple-external-authenticator` package\. 

   ```
   $ sudo apt install ./nice-dcv-simple-external-authenticator_2020.0.87-1_amd64.ubuntu1804.deb
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