# Enabling Touchscreen and Stylus Support<a name="enable-stylus"></a>

Touchscreen is supported with all of the supported Windows operating systems\. Stylus is supported with Windows 10 and Windows Server 2019 only\. The features are enabled by default on Windows NICE DCV servers\. No additional configuration is required\.

Touchscreen and stylus are supported with all of the supported Linux operating systems\. The features are enabled by default on virtual sessions hosted on Linux NICE DCV servers\. However, some additional configuration is required to enable the features on console sessions hosted on Linux NICE DCV servers\.

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

1. To ensure that the input devices are properly configured, run the following command\.

   ```
   $ sudo DISPLAY=:0 xinput
   ```

   The DCV stylus pen, DCV stylus eraser, and DCV ttouchscreen should appear in the command output\. The following is example output\.

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