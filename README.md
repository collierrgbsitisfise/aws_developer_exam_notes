 # AWS DEVELOPER EXAM NOTES

Officical exam guide
[https://d1.awsstatic.com/training-and-certification/docs-dev-associate/AWS_Certified_Developer_Associate-Exam_Guide_EN_1.4.pdf]


# IAM (Identity access management)

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

```javascript
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
 * Roles usualy are not assigned to Users or Groups

Users & Groups

* Users are individual accounts with usernames & passwords; and Access Key ID's and Access Keys
* Groups are collections of users accounts
ie. Developers, Admins, DevOps

* Policies can either be applied to Groups or to individual accounts
* Up to 10 policies per group

The AWS recommend security practice is to use Roles wherever possible to handle authentication for applications. So for example if you have a web server which needs to access RDS instances, and S3 buckets; instead of creating a user for authentication to those resources, and have the AWS Access Key's for that user saved on the web server in a config file somewhere; you would create a role with the relevant policies applied and assign the role to the EC2 instance used by the web server.


<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fscriptcrunch.com%2Fwp-content%2Fuploads%2F2017%2F11%2Faws-iam.jpg&f=1&nofb=1">

# Amazone Elastic Compute Cloud (Amazone EC2)

EC2 - is a web service that rpovide resizable compute capacity in the cloud. You can provision Virtual Machines in a minutes, allowing quickly scale copacity, as your requiremnts load is changed

EC2 Options:

 - On Demand - allows you to pay fixed rate by the hour(or by second) with no commitment.

 - Reserved - provides you with  a capacity reservation and offer a significant discount on the hourly charge for an instance of terms of 1 or 3 year.

 - Spot - enables you bid whatewer price you want for instance capacity, providing for even greater savings if your application have felxibile start and end times.

- Dedicated Hosts - phisical EC2 server dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses.


<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmedia.amazonwebservices.com%2Fblog%2F2013%2Fec2_instance_types_table_1.png&f=1&nofb=1">

<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fscriptcrunch.com%2Fwp-content%2Fuploads%2F2016%2F08%2Finstance-deatils_mini.jpg&f=1&nofb=1">

# Amazone EBS

Amazone EBS allows you to create storage volumes and attach them to Amazone EC2 instance. Once attached, you can create a file system on top of these volumes, run a database, or use them in any other way you would use a block device. Amazone EBS volumes are placed in a specific Availability Zone, where they are automaticaly replicated to protect you from the failure of a single component.

<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fimage.slidesharecdn.com%2Fsqlpass-export-170317032122%2F95%2Fbest-practices-running-sql-server-on-aws-35-638.jpg%3Fcb%3D1489721091&f=1&nofb=1" />

There is a greate article explaining EBS(https://intellipaat.com/blog/what-is-aws-ebs-in-amazon/)

# Elastic Load Balancer (ELB)

ELB - helps to distribute the load between the available computing power (EC2, Lambdas...)


Type Of Load Balancers:
  - Application Load Balancer:
    are best suited for load balancing of HTTP(S) traffic. They operate at layer 7 (https://en.wikipedia.org/wiki/OSI_model).There is possibility to create advanced routing, sending specific request to specific web servers.

  - Network Load Balancer:
    are best suited for load balanacing of TCP traffic where extreme performance is required. Operating at layer 4(https://en.wikipedia.org/wiki/OSI_model). Network Load Balancer are capable to handle up to million of requests per second, while maintaining ultra-low latencies.

  - Classic Load Balancer:
    are the legacy Elastic Load Balancers. You can load balance HTTP/HTTPS applications and use Layer 7 specific features, such as X-Forwarded and sticky sessions. You can also use strict Layer 4 load balancing for applications that on the TCP protocol.


There is a grate article explaining ELB (https://mindmajix.com/what-is-aws-elb)


