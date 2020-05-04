# Licensing the NICE DCV Server<a name="setting-up-license"></a>

The NICE DCV licensing requirements differ depending on where you are installing and using the NICE DCV server\.

**Important**  
The following licensing requirements only apply to NICE DCV version 2017\.0 and later\.

## NICE DCV on Amazon EC2<a name="setting-up-license-ec2"></a>

You do not need a license server to install and use the NICE DCV server on an EC2 instance\. The NICE DCV server automatically detects that it is running on an Amazon EC2 instance and periodically connects to an S3 bucket to determine whether a valid license is available\. 

Make sure that your instance:
+ Can reach the Amazon S3 endpoint\. If it has access to the internet, it connects using the Amazon S3 public endpoint\. If your instance does not have access to the internet, configure a gateway endpoint for your VPC with an outbound security group rule or access control list \(ACL\) policy that allows you to reach Amazon S3 through HTTPS\. For more information, see [Gateway VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-gateway.html) in the *Amazon VPC User Guide*\. If you experience any issues connecting to the S3 bucket, see [Why can’t I connect to an S3 bucket using a gateway VPC endpoint?](https://aws.amazon.com/premiumsupport/knowledge-center/connect-s3-vpc-endpoint/) in the *AWS Knowledge Center*\.
+ Has permission to access the required Amazon S3 object\. Add the following Amazon S3 access policy to the instance's IAM role and replace the *region* placeholder with your AWS Region \(for example, `us-east-1`\)\. For more information, see [Create IAM Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-service.html)\.

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
+ If you are using a Windows instance, ensure that the instance can access the *instance metadata service*\. Access to this service is required to ensure that the NICE DCV server can be properly licensed\. For more information about the instance metadata service, see [Instance Metadata and User Data](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-instance-metadata.html) in the *Amazon EC2 User Guide for Windows Instances*\.

  If you are using a custom Windows AMI, you must install either EC2Config Service \(Windows Server 2012 R2 and earlier\) or EC2Launch \(Windows Server 2016 and later\)\. This ensures that your instance can access the instance metadata service\. For more information, see [Configuring a Windows Instance Using the EC2Config Service](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2config-service.html) or [Configuring a Windows Instance Using EC2Launch](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2launch.html) in the *Amazon EC2 User Guide for Windows Instances*\.

If you are installing and using the NICE DCV server on an Amazon EC2 instance, you can skip the rest of this chapter\. The rest of this chapter only applies to using the NICE DCV server on an on\-premises or alternative cloud\-based server\.

## NICE DCV on On\-premises and Other Cloud\-based Servers<a name="setting-up-license-onprem"></a>

A license is required to install and use the NICE DCV server on an on\-premises or alternative cloud\-based server\. The following licensing options are available:
+ **Automatic evaluation license**— Automatically installed when you install the NICE DCV server\. These licenses are valid for a period of 30 days from the date of installation\. After the license expires, you are no longer able to create and host NICE DCV sessions on the server\. These licenses are ideal for short\-term testing and evaluation\. To test for a longer period, request an extended evaluation license\.
**Note**  
The NICE DCV server defaults to the automatic evaluation license if no other license has been configured\.
+ **Extended evaluation license**— An extended evaluation license is an evaluation license that extends the initial 30\-day evaluation period provided by the automatic evaluation license\. The period is determined by NICE on a case\-by\-case basis\. Extended evaluation licenses become invalid when they reach their expiration date, and you are no longer able to create and host NICE DCV sessions on the server\. Extended evaluation licenses must be requested from a NICE distributor or reseller listed on the [ How to Buy](https://www.nice-software.com/index.html#buy) page of the NICE website\. The licenses come as a license file that must be installed on the NICE DCV server\. 
+ **Production license**—A production license is a full license that you purchase from NICE\. Production licenses are *floating licenses* that are managed by a license server\. Floating licenses allow you to run multiple NICE DCV servers in your network and limit the number of concurrent NICE DCV sessions you can create across all of the servers\. You need one license for each concurrent NICE DCV session\. Production licenses are distributed as a license file that you must install on a Reprise License Manager \(RLM\) server\. There are two types of production licenses: 
  + **Perpetual Licenses**— Perpetual licenses do not have an expiration date and can be used for an indefinite period\.
  + **Subscriptions**— Subscriptions are valid for a limited period of time, typically one year\. The expiration date of the license is indicated in the license file\. After the license expires, you are no longer able to create and host NICE DCV sessions on your NICE DCV servers\.

For information about how to purchase a NICE DCV perpetual license or a subscription, see [How to Buy](https://www.nice-software.com/index.html#buy) on the NICE website and find a NICE distributor or reseller in your region\.

**Note**  
NICE DCV clients do not require a license\.

**Note**  
NICE DCV server version 2020 is not compatible with production license and extended evaluation files from NICE DCV server version 2019 and earlier\. If you upgrade to NICE DCV server version 2020, you must request compatible license files\. For more information, contact your NICE DCV distributor or reseller\.
NICE DCV server version 2020 license files are backward compatible with NICE DCV server versions 2017 and 2019\.
NICE DCV clients do not require a license\.

**Topics**
+ [NICE DCV on Amazon EC2](#setting-up-license-ec2)
+ [NICE DCV on On\-premises and Other Cloud\-based Servers](#setting-up-license-onprem)
+ [Installing an Extended Evaluation License](setting-up-evaluation.md)
+ [Installing a Production License](setting-up-production.md)