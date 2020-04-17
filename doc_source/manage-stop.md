# Stopping the NICE DCV Server<a name="manage-stop"></a>

You can stop the NICE DCV server at any time\. Stopping the server terminates all active NICE DCV sessions\. You can't start new sessions until the server is restarted\.

**Topics**
+ [Stopping the Server on Windows](#manage-stop-windows)
+ [Stopping the Server on Linux](#manage-stop-linux)

## Stopping the NICE DCV Server on Windows<a name="manage-stop-windows"></a>

Use the following procedure to stop the NICE DCV server using the Services snap\-in for the Microsoft Management Console\.

**To stop the NICE DCV server on Windows**

1. Open the Services snap\-in for the Microsoft Management Console\.

1. In the right pane, open **DCV Server**\.

1. Choose **Stop**\.

**Note**  
If the server is already stopped, the **Stop** button is disabled\.

Use the following procedure to disable automatic NICE DCV server startup using the Services snap\-in for the Microsoft Management Console\.

**To prevent the NICE DCV server from starting automatically on Windows**

1. Open the Services snap\-in for the Microsoft Management Console\.

1. In the right pane, open **DCV Server**\.

1. For **Startup service**, choose **Manual**\.

## Stopping the NICE DCV Server on Linux<a name="manage-stop-linux"></a>

Use the following procedure to stop the NICE DCV server using the command line\.

**To stop the NICE DCV server on Linux**  
Use the following commands:
+ RHEL 6\.x and CentOS 6\.x

  ```
  $ sudo service dcvserver stop
  ```
+ RHEL 7\.x, CentOS 7\.x, and SUSE Linux Enterprise 12 

  ```
  $ sudo systemctl stop dcvserver
  ```

Use the following procedure to disable automatic NICE DCV server startup using the command line\.

**To prevent the NICE DCV server from starting automatically on Linux**  
Use the following commands:
+ RHEL 6\.x and CentOS 6\.x

  ```
  $ sudo chkconfig —del dcvserver
  ```
+ RHEL 7\.x, CentOS 7\.x, and SUSE Linux Enterprise 12 

  ```
  $ sudo systemctl disable dcvserver
  ```