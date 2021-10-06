# Enabling touchscreen and stylus support<a name="enable-stylus"></a>

Touchscreens are supported on all of the supported Windows operating systems\. Styluses are supported only on Windows 10 and Windows Server 2019\. By default, the features are enabled on Windows NICE DCV servers\. No additional configuration is required\.

Touchscreens and styluses are supported on all of the supported Linux operating systems\. The features are enabled by default on virtual sessions hosted on Linux NICE DCV servers\. However, some additional configuration is required to enable the features on console sessions hosted on Linux NICE DCV servers\.

Stylus pen pressure and tilt events are supported only on the Windows, Linux, and macOS clients, and a web browser client that's running in a Chromium\-based web browser, such as Edge version 79 and later and Google Chrome\.

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
   + RHEL 7\.x/8\.x, CentOs 7\.x/8\.x, Amazon Linux 2, Ubuntu 18\.x, and SUSE Linux Enterprise 12\.x

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