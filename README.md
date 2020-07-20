 # AWS DEVELOPER EXAM NOTES

Officical exam guide
[https://d1.awsstatic.com/training-and-certification/docs-dev-associate/AWS_Certified_Developer_Associate-Exam_Guide_EN_1.4.pdf]


## IAM (Identity access management)

Essentialy, IAM allows you to manage users and their level of access to the AWS Console. It is important to understand IAM and how it works, both for the exam and for administratioing a comany's AWS account in real life

What does IAM give you ?
 * Centralized control of you AWS account
 * Sahred Access to your AWS account
 * Granual Permissions
 * Identity Federation (including Active Directory, FB,LI, etc)
 * Provide temporary access for users/devices and services, as necessary
 * Allow you to set up your own password rotation policy

Terms:
  * User - End User
  * Group - A collection of users under one set of permissions
  * Role - You create roles and cant assign them to AWS resources
  * Policies - A document that defines (one or more) permissions.

<hr />

So Policies, Roles and Groups... important one to know as it's key to AWS security..

Policies

 * Applied to Roles, Groups or Objects (ie S3)
 * Uses JSON format
 * Describe the level of access applied to an AWS resource by an AWS resource or user

To be more specific Policies either grant or deny the ability to call a specific method on a specific resource in the AWS API.

An example policy below:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow", // Can be either grant or Deny
      "Action": "s3:", // Allows any S3 API method to be called
      "Resource": "*" //  Wildcard, so allows any resource, can be changed to an Amazon Resource Name (ARN)
    },
    {
      "Effect": "Allow",
      "Action": "ec2:Describe",
      "Resource": "*"
    }
  ]
}
```



Roles

 * Used to delegate access to AWS Resources
 * Can be assigned to an AWS Resource (ie EC2 instance) or third party accounts (ie. another AWS account or SAML 2.0)
 * Up to 10 policies can be assigned to a role (this is new, it used to be 2)
 * Roles CANNOT be assigned to Users or Groups

Users & Groups

* Users are individual accounts with usernames & passwords; and Access Key ID's and Access Keys
* Groups are collections of users accounts
ie. Developers, Admins, DevOps

* Policies can either be applied to Groups or to individual accounts
* Up to 10 policies per group

The AWS recommend security practice is to use Roles wherever possible to handle authentication for applications. So for example if you have a web server which needs to access RDS instances, and S3 buckets; instead of creating a user for authentication to those resources, and have the AWS Access Key's for that user saved on the web server in a config file somewhere; you would create a role with the relevant policies applied and assign the role to the EC2 instance used by the web server.
