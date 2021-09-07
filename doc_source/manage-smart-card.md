# Configuring smart card caching<a name="manage-smart-card"></a>

The smart card caching feature enables the NICE DCV server to cache smart card values\. When this feature is enabled, the NICE DCV server caches the results of recent calls to the client's smart card\. Future calls are retrieved directly from the server's cache, instead of from the client\. This reduces the amount of traffic that's transferred between the client and the server and improves performance\. This is especially useful if the client has a slow internet connection\.

By default, smart card caching is disabled\. Clients can manually enable smart card caching for each application they run by setting the `DCV_PCSC_ENABLE_CACHE` environment variable\. For instructions, see [Using a Smart Card](https://docs.aws.amazon.com/dcv/latest/userguide/using-smartcard.html) in the *NICE DCV User Guide*\. Or, you can configure the NICE DCV server to permanently enable or disable smart card caching, regardless of the value specified for the `DCV_PCSC_ENABLE_CACHE` environment variable\.

------
#### [ Linux NICE DCV server ]

**To permanently enable or disable smart card caching on a Linux NICE DCV server**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `enable-cache` parameter in the `[smartcard]` section\. To permanently enable smart card caching, enter `'always-on'`\. To permanently disable smart card caching, enter `'always-off'`\.

   If there's no `enable-cache` parameter in the `[smartcard]` section, add it manually using the following format:

   ```
   [smartcard]
   enable-cache='always-on'|'always-off'
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.

------
#### [ Windows NICE DCV server ]

**To permanently enable or disable smart card caching on a Windows NICE DCV server**

1. Open the Windows Registry Editor\.

1. Navigate to the **HKEY\_USERS/S\-1\-5\-18/Software/GSettings/com/nicesoftware/dcv/smartcard/** key and select the **enable\-cache** parameter\.

   If the parameter doesn't exist, use the following steps to create it:

   1. In the left pane, open the context \(right\-click\) menu for the **smartcard** key, and choose **New**, **String Value**\.

   1. For **Name**, enter `enable-cache` and press **Enter**\.

1. Open the **enable\-cache** parameter\. For **Value data**, enter `always-on` to permanently enable smart card caching, or enter `always-off` to permanently disable smart card caching\.

1. Choose **OK** and close the Windows Registry Editor\.

------