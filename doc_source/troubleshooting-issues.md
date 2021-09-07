# Common Issues<a name="troubleshooting-issues"></a>

This topic lists some common issues\.

**Topics**
+ [Cursor Issues on a Windows NICE DCV Server](#troubleshooting-issues-cursor)
+ [Copy and Paste to IntelliJ IDEA](#troubleshooting-copy-paste-intellij)

## Cursor Issues on a Windows NICE DCV Server<a name="troubleshooting-issues-cursor"></a>

With NICE DCV servers running on Windows Server 2012 or Windows 8 and later, the mouse cursor always appears as an arrow\. This happens even when pausing on text entry fields or single\-click navigation items\. This could happen if there is no physical mouse attached to the server, or if there is no mouse device listed in Device Manager\.

**To resolve the issue**

1. Open Control Panel, and choose **Ease of Access Center**\.

1. Choose **Make the mouse easier to use**\.

1. Select **Turn on Mouse Keys**\. 

1. Choose **Apply**, **OK**\.

## Copy and Paste to IntelliJ IDEA<a name="troubleshooting-copy-paste-intellij"></a>

When trying to copy text from the macOS NICE DCV Client to IntelliJ IDEA, the text cannot be pasted\. IntelliJ can't accept the cross\-platform format that NICE DCV uses by default\. To disable cross\-platform text on NICE DCV so you can paste text into IntelliJ, modify the `disabled-targets` field on the NICE DCV Server\.

This change will prevent copy and paste from working with the NICE DCV web client\. Make sure that you want copy and paste for Intellij IDEA to work on only the NICE DCV Client before making this change\.

**To configure the server to paste text into IntelliJ IDEA**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `disabled-targets` parameter in the `[clipboard]` section\. If there is no `disabled-targets` or `[clipboard]` section, add them manually\.

1. Add the following content to define the value for `disabled-targets`\.

   ```
   [clipboard]
   disabled-targets = ['dcv/text', 'JAVA_DATAFLAVOR:application/x-java-jvm-local-objectref; class=com.intellij.codeInsight.editorActions.FoldingData']
   ```

1. Save and close the file\.

1. [Stop](managing-sessions-lifecycle-stop.md) and [restart](managing-sessions-start.md) the NICE DCV session\.