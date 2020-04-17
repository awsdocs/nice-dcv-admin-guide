# Changing the TLS Certificate<a name="manage-cert"></a>

NICE DCV automatically generates a self\-signed certificate that is used to secure traffic between the NICE DCV client and NICE DCV server\. This certificate is used by default if no other certificate is installed on your NICE DCV server\. The default certificate includes two files, the certificate itself \(`dcv.pem)` and a key \(`dcv.key`\)\.

You can replace the default NICE DCV certificate and its key with your own certificate and key\.

**To change the NICE DCV server's TLS certificate**
+ Windows NICE DCV server

  Place the certificate and its key in the following location on your Windows NICE DCV server:

  ```
  C:\Windows\System32\config\systemprofile\AppData\Local\NICE\dcv\
  ```
+ Linux NICE DCV server

  Place the certificate and its key in the following location on your Linux NICE DCV server:

  ```
  /etc/dcv/
  ```

  Grant ownership of both files to the `dcv` user, and change their permissions to 600 \(only the owner can read or write to them\)\.

  ```
  $  sudo chown dcv certificate_filename.pem key_filename.key
  ```

  ```
  $  sudo chmod 600 certificate_filename.pem key_filename.key
  ```