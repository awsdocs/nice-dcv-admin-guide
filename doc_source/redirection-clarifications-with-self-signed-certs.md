# Redirection clarifications with self\-signed certificates<a name="redirection-clarifications-with-self-signed-certs"></a>

When redirecting to a NICE DCV session from a web\-based portal or application, self\-signed certificates can break the browser trust with the session if the certificate has not been previously trusted\. An example case of this happening is the following:

1. The user connects to the corporate portal site from where the app is loaded\.

1. The app tries to open a direct, secure connection with the NICE DCV Server using a self\-signed certificate\.

1. The browser denies the secure connection because the certificate is self\-signed\.

1. The user doesn't see the remote server because the connection wasn't established\.

The trust issue is specific to step 3\. When a user connects to a website with a self\-signed certificate \(e\.g\. navigating to https://example\.com\) the browser asks to trust the certificate\. However, if a web app/page, served either via HTTP or HTTPS, tries to establish a secure WebSocket connection to DCV server\. If the certificate is self\-signed, the browser checks if it was previously trusted\. If it was not previously trusted, it denies the connection without prompting the user with the request if they want to trust the certificate\.

Possible solutions in this case:
+ Have a valid certificate for the DCV Server machine if the business is using a custom domain for its machine\. For the certificate, they could distribute an enterprise certificate to DCV\.  
**Example**  

  User \-\-\-\[valid certificate\]\-\-\-> DCV Server instance
+ Secure the DCV Servers fleet under a proxy/gateway\. In only this case, the proxy/gateway needs to have a valid certificate and the DCV Server instance can keep its self\-signed certificate\. For this option, they can use the [DCV Connection Gateway](https://docs.aws.amazon.com/dcv/latest/gw-admin/what-is-gw.html), an ALB/NLB, or another proxy solution\.  
**Example**  

  User/Cx \-\-\-\[here we need a valid certificate\]\-\-\-> Proxy/Gateway\-\-\-\[self\-signed certificate\]\-\-\-> DCV Server instance
+ Have the user trust the self\-signed certificate before starting the connection via the [SDK](https://docs.aws.amazon.com/dcv/latest/websdkguide/render-ui.html)\. This should be possible by just opening this URL in another tab/window/popup: `https://example.com/version`\.
**Note**  
The /version end\-point will reply with a simple webpage for the DCV server version under an HTTPS connection\.

  The same self\-signed certificate can be used later in the actual DCV Server connection\.