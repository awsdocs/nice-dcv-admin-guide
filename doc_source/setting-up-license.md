# Licensing NICE DCV<a name="setting-up-license"></a>

The NICE DCV licensing requirements differ depending on where you are installing and using the NICE DCV server\.

## NICE DCV on Amazon EC2<a name="setting-up-license-ec2"></a>

You do not need a license server to install and use the NICE DCV server on an EC2 instance\. The NICE DCV server automatically detects that it is running on an Amazon EC2 instance and periodically connects to an Amazon S3 bucket to determine whether a valid license is available\. 

Make sure that your instance:
+ Can reach the Amazon S3 endpoint\. If it has access to the internet, it connects using the Amazon S3 public endpoint\. If your instance does not have access to the internet, configure a gateway endpoint for your VPC with an outbound security group rule or Access Control List \(ACL\) policy that allows you to reach Amazon S3 via HTTPS\. For more information, see [Gateway VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-gateway.html) in the *Amazon VPC User Guide*\. If you experience any issues connecting to the Amazon S3 bucket, see [Why can’t I connect to an S3 bucket using a gateway VPC endpoint?](https://aws.amazon.com/premiumsupport/knowledge-center/connect-s3-vpc-endpoint/) in the *AWS Knowledge Center*\.
+ Has permission to access the required Amazon S3 object\. Add the following Amazon S3 access policy to the instance's IAM role and replace the *region* placeholder with your region, for example `us-east-1`\. For more information, see [Create IAM Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html)\.

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": "s3:GetObject",
              "Resource": "arn:aws:s3:::dcv-license.region/*"
          }
      ]
  }
  ```

If you are installing and using the NICE DCV server on an Amazon EC2 instance, you can skip the rest of this chapter\. The rest of this chapter only applies to using the NICE DCV server on an on\-premises or alternative cloud\-based server\.

## NICE DCV on On\-premises and Other Cloud\-based Servers<a name="setting-up-license-onprem"></a>

A license is required to install and use the NICE DCV server on an on\-premises or alternative cloud\-based server\. The following licensing options are available:
+ **Automatic demo license**— Automatically installed when you install the NICE DCV server\. These licenses are valid for a period of 15 days from the date of installation\. After the license expires, you are no longer able to create and host NICE DCV sessions on the server\. These licenses are ideal for short\-term testing\. To test for a longer period, request an extended demo license\.
**Note**  
The NICE DCV server defaults to the automatic demo license if no other license has been configured\.
+ **Extended demo license**—An extended demo license is a demo license that is valid for a period longer than 15 days\. The period is determined by NICE on a case\-by\-case basis\. Extended demo licenses become invalid when they reach their expiration date, and you are no longer able to create and host NICE DCV sessions on the server\. Extended demo licenses must be requested from NICE\. They come as a license file that must be installed on the NICE DCV server\. 
+ **Floating license**—A floating license is a full license that you purchase from NICE\. Floating licenses do not have an expiration date and can be used for an indefinite period\. However, they do limit the number of sessions that you can host on the NICE DCV server concurrently\. These licenses come as a license file to be installed on a Reprise License Manager \(RLM\) server\.

For more information about licenses, see the [NICE](https://www.nice-software.com/contacts/demo-license) website\.

**Note**  
NICE DCV clients do not require a license\.

**Topics**
+ [NICE DCV on Amazon EC2](#setting-up-license-ec2)
+ [NICE DCV on On\-premises and Other Cloud\-based Servers](#setting-up-license-onprem)
+ [Installing an Extended Demo License](setting-up-demo.md)
+ [Installing a Floating License](setting-up-floating.md)