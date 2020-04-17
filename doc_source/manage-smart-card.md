# Configuring Smart Card Caching<a name="manage-smart-card"></a>

The smart card caching feature enables the NICE DCV server to cache smart card values\. When this feature is enabled, the NICE DCV server caches the results of recent calls to the client's smart card\. Future calls are retrieved directly from the server's cache, instead of from the client\. This helps to reduce the amount of traffic that is transferred between the client and the server and improves performance\. It is especially useful if the client has a slow internet connection\.

**Note**  
Smart card functionality is only supported with Linux NICE DCV servers\.

Smart card caching is disabled by default\. Clients can manually enable smart card caching for each application they run by setting the `DCV_PCSC_ENABLE_CACHE` environment variable\. For more information, see [Using a Smart Card](https://docs.aws.amazon.com/dcv/latest/userguide/using-smartcard.html) in the *NICE DCV User Guide*\. Or, you can configure the NICE DCV server to permanently enable or disable smart card caching, regardless of the value specified for the `DCV_PCSC_ENABLE_CACHE` environment variable\.

**To permanently enable or disable smart card caching**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `enable-cache` parameter in the `[smartcard]` section\. To permanently enable smart card caching, enter `'always-on'`\. To permanently disable smart card caching, enter `'always-off'`\.

   If there is no `enable-cache` parameter in the `[smartcard]` section, add it manually using the following format:

   ```
   [smartcard]
   enable-cache='always-on'|'always-off'
   ```

1. Save and close the file\.

1. [Stop](manage-stop.md) and [restart](manage-start.md) the NICE DCV server\.