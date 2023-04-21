# Enabling touchscreen and stylus support<a name="enable-stylus"></a>

**Note**  
 USB redirection for touchscreen and stylus devices is not needed\. Also, no vendor drivers need to be installed on the NICE DCV server\.  
NICE DCV supports touchscreen and stylus by using the native operating system APIs\.  
Windows uses Windows Ink\.  
Linux uses X11 input injection\.
+ **Windows servers support**

  Touchscreens are supported on all of the supported Windows operating systems\. Styluses are supported on all the supported Windows operating systems starting from Windows 10 and Windows 2019, they are not supported on Windows 2016, Windows 8\.1 and older versions\. By default, the features are enabled on Windows NICE DCV servers\. No additional configuration is required\. 
+ **Linux servers support**

  Touchscreens and styluses are supported on all of the supported Linux operating systems\. The features are enabled by default on virtual sessions hosted on Linux NICE DCV servers\. However, some additional configuration is required to enable the features on console sessions hosted on Linux NICE DCV servers\. 

**Important**  
 Touchscreen and stylus use with NICE DCV is enabled if the feature is supported *on both client and server*, and enabled on the server\. For information about client support, see [the client features](https://docs.aws.amazon.com/dcv/latest/userguide/client.html#client-features) in the *NICE DCV User Guide*\. 

**To enable touchscreen and stylus support for console sessions hosted on a Linux NICE DCV server**

1. Open `/etc/X11/xorg.conf` using your preferred text editor\.

1. Add the following sections to the file\.

   ```
   Section "InputDevice"
     Identifier "DCV Stylus Pen"
     Driver "dcvinput"
   EndSection
   
   Section "InputDevice"
     Identifier "DCV Stylus Eraser"
     Driver "dcvinput"
   EndSection
   
   Section "InputDevice"
     Identifier "DCV Touchscreen"
     Driver "dcvinput"
   EndSection
   ```

1. Add the following to the end of the `ServerLayout` section\.

   ```
   InputDevice  "DCV Stylus Pen"
   InputDevice  "DCV Stylus Eraser"
   InputDevice  "DCV Touchscreen"
   ```

   For example:

   ```
   Section "ServerLayout"
     ...existing content...
     InputDevice  "DCV Stylus Pen"
     InputDevice  "DCV Stylus Eraser"
     InputDevice  "DCV Touchscreen"
   EndSection
   ```

1. Save the changes and close the file\.

1. Restart the X server\.
   + RHEL, CentOS, Amazon Linux 2, Ubuntu 18\.x, and SUSE Linux Enterprise 12\.x

     ```
     $ sudo systemctl isolate multi-user.target
     ```

     ```
     $ sudo systemctl isolate graphical.target
     ```

1. To ensure that the input devices are properly configured, run the following command\.

   ```
   $ sudo DISPLAY=:0 xinput
   ```

   The DCV stylus pen, DCV stylus eraser, and DCV touchscreen appears in the command output\. The following is example output\.

   ```
   | Virtual core pointer                          id=2    [master pointer  (3)]
   |   | Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
   |   | dummy_mouse                               id=6    [slave  pointer  (2)]
   |   | dummy_keyboard                            id=7    [slave  pointer  (2)]
   |   | DCV Stylus Pen                            id=8    [slave  pointer  (2)]
   |   | DCV Stylus Eraser                         id=9    [slave  pointer  (2)]
   |   | DCV Touchscreen                           id=10   [slave  pointer  (2)]
   | Virtual core keyboard                         id=3    [master keyboard (2)]
       | Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
   ```

## Configuring a stylus pressure range<a name="config-stylus-pressure"></a>

There are some applications that require you to reduce the stylus pressure range to between 0 and 2048\. You can configure the pressure range by setting the `Pressure2k` option to true in the `/etc/X11/xorg.conf` file\.

**To configure stylus pressure**

1. Open `/etc/X11/xorg.conf` using your preferred text editor\.

1. Add the following sections to the file\.

   ```
   Section "InputDevice"
     Identifier "DCV Stylus Pen"
     Driver "dcvinput"
     Option "Pressure2K" "true"
   EndSection
   
   Section "InputDevice"
     Identifier "DCV Stylus Eraser"
     Driver "dcvinput"
     Option "Pressure2K" "true"
   EndSection
   ```

1. Save the changes and close the file\.

1. Restart the X server\.