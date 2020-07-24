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

# Route53

Route53 - is Amazon's DNS server

Allows to map domain name to:
  - EC2 Instances
  - Load Balancers
  - S3 Buckets

There is article about Route53: https://cloudacademy.com/blog/route53-dns-migration/ , but i would say it's more needed for AWS associate solutions architect exam.

# RDS

Amazon RDS is the Relational Database Service offered as a web service by Amazon. It makes it easy to set-up and operate a relational database in the cloud. It provides a very cost-effective way to use industry’s leading RDBMS software as a managed service. Because of this web service from amazon AWS, You do not have to buy any server or install any database software in it. You just have subscribe to the AWS RDS web service and start using the RDBMS features after some initial configuration involving memory and CPU capacity allocation etc . In this Tutorial we will learn about the different interfaces available in AWS RDS to use the industry’s leading RDBMS software.

As RDS is a managed service provided by AWS, we can expect that like other AWS services it will provide scalability, security and cost effectiveness to the various RDBMS it provides. The database products available through AWS RDS are as listed below.

 * MySQL - Support versions for MySQL 5.5 to 5.7. Minor upgrades happen  automatically without needing any involvement from the user.

 * MariaDB – Support versions for MariaDB from 10.0 to 10.2.

 * Oracle – Supports version 11g and 12c. You can use the oracle license provided by aws or bring your own license. The costing for these two are different.

 * Microsoft SQL Server – Supports version 200t to 2017. Also AWS supports the various editions like – Enterprise, Standard, Web and Express.

 * PostgreSQL – Supports version 9 to 11. Can be configured as a multi A-Z deployment with read replicas.

 * Amazon Aurora – This is Amazon’s own RDBMS. We will be covering it in a separate tutorial.

Each of these Database software is offered as Software as a Service (saas) by providing following features.

 * Customization of CPU capacity, Memory allocation and IOPS(Input Output per second) for a database instance.

 * Manage software patching, failure and recovery of the RDBMS software without any user intervention.

 * Allow manual or automated backup of the database using snapshots. Restore the database from these snapshots.

 * Provide high availability by creating a primary and secondary instance which are synchronous. In case of a failure of primary AWS RDS automatically fails over to secondary.

 * Put the databases in a virtual private cloud (VPC) and aslo use AWS IAM (Identity and Access management) service to control access to the databases.

 * There are two purchase options for AWS RDS service. On-Demand Instances and Reserved Instances. For on-Demand instance you pay for every hour of usage while for Reserved instance you make a upfront payment for one year to three period time frame.

 resource of **this** RDS part was provided by: https://www.tutorialspoint.com/amazonrds/amazonrds_overview.htm

### Automated backup

**T**here are two types of Backup for AWS: Automated Backup and Database Snapshots.

**A**utomated Backup allows you to recover your database at any point in time within a "retention preriod". The retention period can be between one and 35 days. Automated Backup will take a full daily snapshot and will also store transaction logs throughout the day. When you do a revovery, AWS will first choose the most recent daily backup, and then apply transaction logs relevant to that day. This allows you to do a point in time revovery to a second, within the retation period.

**S**napshots are done manually. They are stored even after you delete the original RDS instance, unlike automated backups.

### Multi-AZ RDS
Multi-AZ RDS allows you to have an exact copy of your production database in another Availability Zone. AWS handles the replication for you. In the case DB will fail Amazone RDS will automaticly failover to the standby so the database operations can resume quickly without administrative intervetion.

**!!!** Multi-AZ is for **Disaster Recovery** only. It is not used for performance improving, for that you need to use **Read Replica**

### Read Replica

Read Replica allow you to have a read-only copy of your production database. This is achived by using ASynchronouse replication from the primary RDS instance to the read replica.You use read replica primarly for very-heavy database workloads.

# ElasticCache

ElasticCache is a web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud. The service improves the performance of web apllication by allowing you to retrive information from fast, managed, in-memory caches, instead of relying entirely on slower disk-based databases.

Common use cases of Redis usage(http://highscalability.com/blog/2011/7/6/11-common-web-use-cases-solved-in-redis.html)

Types of elasticcache:

  * Memcached(https://www.memcached.org/)
  * Redis(https://redis.io/)

Although both  Memcached and Redis appear similar on the surface (in that are both in-memory key space), they are actiualy quite different in practice. Because of the replication abd presistence feature of Redis, ElasticCache manages Redis more as stateful database. Redis ElasticCache manages Redis more as stateful enitities that include failover, similar to how Amazone RDS manages database failover.

Because Memcached is a designed as a pure caching solution with no persistence, Elastic manages Memcached nodejs as pool that can grow and shrink, similar to an Amazone EC2 Auto Scaling Group. Individual nodes are expendable and ElasticCache provides additional capabililities here, such as automatic node replacement and Auto Discovery.

Memcached use cases:
 * Is object caching your primary goal, for example to offload your database ? 

 * Are you interested in as simple caching model as possible ?

 * Are planing on running large cache nodes and  require multithreaded performance with utilization of multiple cores ?

 * Do you want the ability to scale you cache horizontaly as you grow ?

Redis use cases:

  * Are you looking for more advanced data types, such as lists, hases and sets ?

  * Does sorging and ranking datasests in memory help you, such as with leaderboards ?

  * Is persistence of your key store important ? 

  * Do you want to run im multiple AWS Availability Zone with failover ?
