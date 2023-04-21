# Starting the NICE DCV Server<a name="manage-start"></a>

The NICE DCV server must be running to host sessions\.

By default, the NICE DCV server starts whenever the server that it's hosted on starts up\. If you chose to disable automatic startup when you installed the NICE DCV server, you must start the server manually or set up automatic startup again\. To do either option, follow one of these procedures\.

------
#### [ Windows NICE DCV server ]

Manually start the NICE DCV server using the Services snap\-in for the Microsoft Management Console\.

**To start the NICE DCV server on Windows**

1. Open the Services snap\-in for the Microsoft Management Console\.

1. In the right pane, open **DCV Server**\.

1. Choose **Start**\.

**Note**  
If the server is already up and running, the **Start** button is disabled\.

Configure automatic startup using the Services snap\-in for the Microsoft Management Console\.

**To configure the NICE DCV server to start automatically on Windows**

1. Open the Services snap\-in for the Microsoft Management Console\.

1. In the right pane, open **DCV Server**\.

1. For **Startup service**, choose **Automatic**\.

------
#### [ Linux NICE DCV server ]

Manually start the NICE DCV server using the command line\.

**To start the NICE DCV server on Linux**  
Use the following commands:
+ RHEL, CentOS, SUSE Linux Enterprise 12, and Ubuntu 18\.x

  ```
  $ sudo systemctl start dcvserver
  ```

Configure the NICE DCV server to start automatically using the command line\.

**To configure the NICE DCV server to start automatically on Linux**  
Use the following commands:
+ RHEL, CentOS, SUSE Linux Enterprise 12, and Ubuntu 18\.x

  ```
  $ sudo systemctl enable dcvserver
  ```

------