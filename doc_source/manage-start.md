# Starting the NICE DCV Server<a name="manage-start"></a>

The NICE DCV server must be running in order to host sessions\.

By default, the NICE DCV server is configured to start automatically when the server it is hosted on starts up\. If you chose to disable automatic startup when you installed the NICE DCV server, you must start the server manually using the following procedures\.

**Topics**
+ [Starting the Server on Windows](#manage-start-windows)
+ [Starting the Server on Linux](#manage-start-linux)

## Starting the NICE DCV Server on Windows<a name="manage-start-windows"></a>

Use the following procedure to manually start the NICE DCV server using the Services snap\-in for the Microsoft Management Console\.

**To start the NICE DCV server on Windows**

1. Open the Services snap\-in for the Microsoft Management Console\.

1. In the right pane, open **DCV Server**\.

1. Choose **Start**\.

**Note**  
If the server is already running, the **Start** button is disabled\.

Use the following procedure to configure the NICE DCV server to start automatically using the Services snap\-in for the Microsoft Management Console\.

**To configure the NICE DCV server to start automatically on Windows**

1. Open the Services snap\-in for the Microsoft Management Console\.

1. In the right pane, open **DCV Server**\.

1. For **Startup service**, choose **Automatic**\.

## Starting the NICE DCV Server on Linux<a name="manage-start-linux"></a>

Use the following procedure to manually start the NICE DCV server using the command line\.

**To start the NICE DCV server on Linux**  
Use the following commands:
+ RHEL 6\.x and CentOS 6\.x

  ```
  $ sudo service dcvserver start
  ```
+ RHEL 7\.x, CentOS 7\.x, SUSE Linux Enterprise 12, and Ubuntu 18\.x

  ```
  $ sudo systemctl start dcvserver
  ```

Use the following procedure to configure the NICE DCV server to start automatically using the command line\.

**To configure the NICE DCV server to start automatically on Linux**  
Use the following commands:
+ RHEL 6\.x and CentOS 6\.x

  ```
  $ sudo chkconfig —add dcvserver
  ```
+ RHEL 7\.x, CentOS 7\.x, SUSE Linux Enterprise 12, and Ubuntu 18\.x

  ```
  $ sudo systemctl enable dcvserver
  ```