# Configuring the Clipboard on a Linux NICE DCV Server<a name="manage-clipboard"></a>

Linux operating systems feature two buffers that you can use when copying and pasting content: the primary selection and the clipboard\. To copy content into the primary selection, highlight the content using the mouse cursor\. To then paste it from the primary selection, use either the mouse's middle button or the **Shift\+Insert** keyboard shortcut\. To copy content into the clipboard, highlight the content and select **Copy** from the context \(right\-click\) menu\. To paste it from the clipboard, select **Paste** from the context \(right\-click\) menu\.

On a Linux NICE DCV server, you can configure the server to use either the primary selection or clipboard when performing copy and paste actions between the client and the server\.

**Topics**
+ [Pasting Client Clipboard Content to the Primary Selection](#manage-clipboard-paste)
+ [Copying Primary Selection Content to the Client Clipboard](#manage-clipboard-copy)

## Pasting Client Clipboard Content to the Primary Selection<a name="manage-clipboard-paste"></a>

By default, content that is copied in the client is placed in the clipboard\. To paste this content on the server, you must paste it from the clipboard using the context \(right\-click\) menu\.

You can configure the server to place the clipboard content into the primary selection\. This enables users to paste the copied content from both the clipboard, using the context \(right\-click\) menu, and the primary selection, using either the mouse's middle button or the **Shift\+Insert** keyboard shortcut\.

**To configure the server to place clipboard content into the primary selection**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `primary-selection-paste` parameter in the `[clipboard]` section and set the value to `true`\.

   If there is no `primary-selection-paste` parameter in the `[clipboard]` section, add it manually using the following format:

   ```
   [clipboard]
   primary-selection-paste=true
   ```

1. Save and close the file\.

1. [Stop](managing-sessions-lifecycle-stop.md) and [restart](managing-sessions-start.md) the NICE DCV session\.

## Copying Primary Selection Content to the Client Clipboard<a name="manage-clipboard-copy"></a>

By default, users can copy content only from the server to the client using the clipboard\. This means that content copied into the primary selection cannot be pasted on the client\.

You can configure the server to place the primary selection content into the clipboard\. This means that when a user copies content to the primary selection on the server, the content is also copied into the clipboard\. This enables the user to paste the content from the clipboard into the client\.

**To configure the server to place primary selection content into the clipboard**

1. Navigate to `/etc/dcv/` and open the `dcv.conf` with your preferred text editor\.

1. Locate the `primary-selection-copy` parameter in the `[clipboard]` section and set the value to `true`\.

   If there is no `primary-selection-copy` parameter in the `[clipboard]` section, add it manually using the following format:

   ```
   [clipboard]
   primary-selection-copy=true
   ```

1. Save and close the file\.

1. [Stop](managing-sessions-lifecycle-stop.md) and [restart](managing-sessions-start.md) the NICE DCV session\.