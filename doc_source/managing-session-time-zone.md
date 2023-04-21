# Managing session time zone<a name="managing-session-time-zone"></a>

DCV allows session owners and users to set the time zone of their session to reflect either the location of the DCV Server or their current location\.

**Enabling time zone redirection**  
You can enable and disable this feature for all users on a specific session\.

1. Modify the [`enable-timezone-redirection`](config-param-ref.md#paramref.redirection.enable-timezone-redirection) parameter to one of the following values:
   + `always-on`: Time Zone Redirection is always enabled\.

     The feature will be turned on and the session displays the time zone information of the client\. The user will not be able to turn the feature off\.
   + `always-off`: Time Zone Redirection is always disabled\.

     The feature will be turned off and the session displays its own time zone information\. The user will not be able to turn the feature on\.
   + `client-decides`: Time Zone Redirection is turned on by default\.

     The session will have the feature enabled, display the client time zone, and the user will have the option to disable it allowing the server time zone to be displayed\.
**Note**  
This setting is the standard default setting\.
**Note**  
 If only individual users in a session are required to have this feature, you will need to set the centralized parameter for all users first and then adjust individuals’ permissions separately by creating a custom permissions file at [Add permissions](security-authorization-file-create.md#security-authorization-file-create-permission)\. 

1. Restart any affected sessions for your changes to appear\.