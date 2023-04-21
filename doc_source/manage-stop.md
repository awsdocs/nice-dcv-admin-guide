# Stopping the NICE DCV Server<a name="manage-stop"></a>

You can stop the NICE DCV server at any time\. Stopping the server terminates all active NICE DCV sessions\. You can't start new sessions until after the server is restarted\.

------
#### [ Windows NICE DCV server ]

Manually stop the NICE DCV server using the Services snap\-in for the Microsoft Management Console\.

**To stop the NICE DCV server on Windows**

1. Open the Services snap\-in for the Microsoft Management Console\.

1. In the right pane, open **DCV Server**\.

1. Choose **Stop**\.

**Note**  
If the server is already stopped, the **Stop** button is disabled\.

Disable automatic startup using the Services snap\-in for the Microsoft Management Console\.

**To prevent the NICE DCV server from starting automatically on Windows**

1. Open the Services snap\-in for the Microsoft Management Console\.

1. In the right pane, open **DCV Server**\.

1. For **Startup service**, choose **Manual**\.

------
#### [ Linux NICE DCV server ]

Stop the NICE DCV server using the command line\.

**To stop the NICE DCV server on Linux**  
Use the following commands:
+ RHEL, CentOS, and SUSE Linux Enterprise 12 

  ```
  $ sudo systemctl stop dcvserver
  ```

Disable automatic NICE DCV server startup using the command line\.

**To prevent the NICE DCV server from starting automatically on Linux**  
Use the following commands:
+ RHEL, CentOS, and SUSE Linux Enterprise 12 

  ```
  $ sudo systemctl disable dcvserver
  ```

------