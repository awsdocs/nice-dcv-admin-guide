# Using the Command Line Tool to Manage NICE DCV Sessions<a name="managing-sessions-cli"></a>

The NICE DCV server includes a command line tool that can be used to start, stop, and view NICE DCV sessions\.

## Using the Command Line Tool on a Windows NICE DCV Server<a name="cli-win"></a>

To use the command line tool on a Windows NICE DCV server, you must run the commands from the NICE DCV installation directory or you must add the NICE DCV directory to the PATH environment variable\. If you add the NICE DCV directory to the PATH environment variable, you can use the commands from any directory\.

**To use the command line tool from the NICE DCV installation directory**  
Navigate to the folder in which the `dcv.exe` file is located, `C:\Program Files\NICE\DCV\Server\bin\` by default, and open a command prompt window\.

Or you can specify the full path when running a command from a different directory\. For example:

```
C:\> "C:\Program Files\NICE\DCV\Server\bin\dcv.exe" list-sessions
```

**To add the NICE DCV directory to the PATH environment variable**

1. In File Explorer, right\-click **This PC** and choose **Properties**\.

1. Choose **Advanced system settings**\.

1. On the **Advanced** tab, choose **Environment Variables**\.

1. In the **System variables** section, select the **Path** variable and choose **Edit**\.

1. Choose **New** and specify the full path to the `bin` folder in the NICE DCV installation directory \(for example, `C:\Program Files\NICE\DCV\Server\bin\`\)\.

1. Choose **OK** and close the Environment Variables window\.

## Using the Command Line Tool on a Linux NICE DCV Server<a name="cli-lin"></a>

On Linux NICE DCV servers, the command line tool is automatically configured in the `$PATH` environment variable\. This enables you to use the command line tool from any folder\. Open a terminal window and enter the command to run\.