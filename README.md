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


<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fimage.slidesharecdn.com%2Fdat204-151008030810-lva1-app6892%2F95%2Fdat204-nosql-no-worries-build-scalable-apps-on-aws-nosql-services-23-638.jpg%3Fcb%3D1444273964&f=1&nofb=1">

# S3

S3 provides developers and IT teams with  secure, durable, highly-scalable object storage. Amazone S3 is easy to use, with a simple web service interface to store and retrive any amount of data from anywhere on the web

### Data consistancy Model for S3

* Read after Write consistancy for PUT of new Objects
* Eventualy Consistancy for overwrite PUTS and DELETE(can take some time to propogate)


S3 is Object based. Objcet consist of the following:
  - Key(This is simply the name of the object)
  - Value(This is simply the data, which is made up of a sequence of bytes)
  - Version ID (Important for versioning)
  - Metadata (Data about the data you are storing)
  - Subresourcer:
      * Bucket Polices, Access Control Lists
      * Cross Origin Resource Sharing (CORS)
      * Transfer Acceleration

### S3 - storage classes

  * S3: 99.99% availability, 99.999999999% durability, stored redundantly across multiple devices in multiple facilities, and is designed to sustain the loss of 2 facilities concurrrently.
  * S3 -  IA(Infequntly Accessed): For data that accessed less frequently but requires rapid access when needed, Lower fee than S3, but you are charged a retrieval fee.
  * S3 - One Zone IA: Same as IA however data is stored in a single AZ only, still 99.999999999% durability, but only 99.5% availability. Cost is 20% less than regular S3 - IA.
  * Reduced Redundancy Storage: Designed to provide 99.99% durablility and 99.99% avalability.
 * Glacier - very cheep, but used for archival only. Optimised for data that is infrequently accessed and it take 3 - 5 hours to restore from Glacier.

 <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fi1.wp.com%2Fjayendrapatil.com%2Fwp-content%2Fuploads%2F2016%2F03%2Fscreen-shot-2016-03-29-at-8-16-24-am.png%3Fresize%3D656%252C208&f=1&nofb=1">

 ### S3 - security

  * By default all newly created buckets are PRIVTE
  * You can set up access control to you buckets using:
      - Buckets Policies - Applied at a bucket level
      - Access Controll List - Applied at an object level
  * S3 buckets can configured to create a   ccess logs, which log all requests made to the s3 bucket. These logs can be written to another bucket.

### S3 - encryption 
  - In Transit:
    * SSL/TLS

  - At Rest:
    * S3 Managed Keys - ***SSE-S3***
    * AWS Key Management Service, Managed Keys, ***SSE-KMS***
    * Server Side Encryption with Customer Provided Keys - ***SSE-C***

  -  Client Side Encryption

  If you want to enforce the use of encryption for your files stored in S3 use an S3 Bucket Policy to deny all PUT request that don't include the `x-amz-server-side-encryption` in the request header.

# Cloudfront (AWS CDN)

What is CDN ?

 CDN(content dilevery network) is a systen of distributed servers(network) that delivery webpages and other web contentto a user based on the geographic location of the user, the origin of the webpage and ontent deliver server.


CloudFront - Key terminology

  * Edge Location - This is the location where content is cached and can also be writen. Separate to an AWS Region/AZ

  * Origin - This is the origin of all files that the CDN will distribute. Origins can be an S3 Bucket, an EC2 Instance, an Elastic Load Balancer or Route53.

  * Distribution - This is the name given the CDN, which consists of a collection of Edge Locations.

  * Web Destribition - Typically used fo Website.

  * RTMP - Used for Media Streaming.

### Cloudfront and S3 Transfer Acceleration

Amazone S3 Transfer Acceleration enables fast, easy and secure transfer of files over long distances between your end user and an S3 bucket.

Transfer Acceleration takes advantage of Amazone CloudFront's globallydistribituted edge locations. As the data arrives at an edge location. data is routed to Amazone S3 over an optimized network path.

### S3 Performance Optiomizations

* GET-intensive Workload - Use CloudFront
* Mixed-Workload - Avoid sequential key names for your S3 objects. Instead add a random prefix like a hex hash to the key name to prevent multiple objects from being stored on the same partition.


# Serverless

https://brandlitic.com/what-is-serverless-architecture/

https://www.experfy.com/blog/choosing-a-serverless-architecture-for-application-development/

also pretty much recommend all articles from `serverless-transformation`: https://medium.com/serverless-transformation

## Lambda

**AWS Lambda** is a compute service where you can upload your code and create Lambda function. AWS Lambda takes care of provisionning and monitoring the servers that you use to run the code. You don't have to worry about operating systems, pathcing, scaling,  etc. You can use Lambda in the following ways.

 * As an event-driven compute service where AWS Lambda runs your code in response to events. These events could be changes to data in an Amazone S3 bucket or an Amazone DynamoDB table.
 * As a comute service to run your code in response to HTTP requests using Amazone API Gateway or API calls made using AWS SDKs.

 Lambda exam tips:
  
  - Lambda scales out(not up) automatically
  - Lambda functions are independent, 1 event = 1 funciton
  - Lambda a serverless
  - Lambda function can trigger other lambda functions, 1 event can = x functions.

  - Architectures can get extremely complicated, AWS X-ray allows you to debug waht is happening
  - Lambda can do things globally, you can use it to back up S3 buckets to other S3 buckets etc

## Versioning

When you use **versioning** in AWS Lambda, you can publish one or more versions of your Lambda function. As a result, you can work with different variations of your Lambda function in your development workflow, such as development, beta and production.

Each Lambda function version has a unique Amazone REsource Name(ARN). After you publish a verison, it is immutable(that is it cat't be changed)

- Could be multiple versions of lambda function
- Latest version will use **$LATEST**
- Qualified verison will use **$LATEST**, uniquealified will not have it.
- Can split traffic using aliases to different versions
- Can not split trafic with **$LATEST**, insted create an alias to lates

## Step Function

SF - allows you to visualize and test your serverless application. Step Function provides a graphical console to arrange and visualize the components of your application as a series of steps. This makes it simple to build and run multistep applications. Step Function automatically triggers and tracks each step and retries when there are erros, so your application executes in order and as expected. Step Function logs the state of each step, so when things do go wrong you can diagnose nad debug problems quickl.

SP:
 - Greate way to visualize your serverless application
 - Step Function automatically triggers and track each step
 - Step Fcuntions logs the state of each step so if something goes wrong you can track what went wrong.

## AWS X-RAY

AWS X-RAY is a service that collects data about requests that your application serves and provide tools you can use to view, fileter and gain insights into that dta to identify issues and opportunities for optimization. For any traced request to your application you can see detailed information not only about the request and response but also about calls, that your application makes to downstream AWS resoureces, microservices, databases and HTTP web APIs.

X-RAY integrates with the following AWS services:
  * Elastic Load Balancing
  * AWS Lambda
  * Amazone API Gateway
  * Amazone EC2
  * AWS Elastic Beanstalk

# DynamoDB

DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit mulliseconds latency at any scale. It is a fully managed database and supports both document and key-value data models. Is is flexible data model and relible performance make it great fit for modbile, web, gamin, ad-tech, IoT applications.

Consistency  models:

 **Eventually Consistent Reads**: Consistancy across all copies of data usually reached within a second. Repeating a read after a short time should return the updated data. (Best Read Performance)

 **Strongly Consistent Reads**: A strongly consistant read returns a result that reflects all writes that received a successful response prior to the read.
 
## DynamoDB - Primary Keys

* DynamoDB stores and retrives data based on a Primary Key

* 2 types of Primary Key:
  - **Partition Key** - unique attribute(e.g userID). Value of the Partition key us input to an internal hash function which determines the partition of physical location on which the data is stored. If you are using the Partition Key as your Primary Key, then no two items can have the same Partition Key.

  - **Composite Key(Partition Key + Sort Key)** - For example: The same user posting multiple times to a forum. Partition Key is **UserId** and Sort key if **timestamp** (time when post was published). Few items may have the same Partition Key, but must have a different Sort Key. All Items within the same Partition Key are stored together, then sorted according to the Sort Key value.

## DynamoDB Access Control

* Authintication and Access Control is managed using AWS IAM

* You can create IAM user within your AWS account which has specific permissions to access and create DynamoDB tables.

* You can create IAM role which enables you to obtain temporary access keys which can be used to access DynamoDB.

* You can also use a special IAM Condition to restrict a user access to only their own records.

## Indexies

There is two type of indexies:
 * Local Secondary Index
 * Glabal Secondary Index

**Local Secondary Index**:
 - Can only be created when are creating a table
 - You can not add, remove or modify it later
 - It has the same Partition Key as your original table, but different sort key
 - Gives you a different view of your data, organised according to an alternative Sort Key
 - Any queries based on this Sort Key are much faster using the index than main table
 For example with our user table one of local secondary idnex could be: Partition Key - User ID, Sort Key - account creation date.

 **Global Secondary Index**

- You can create when you create your table or add it later
- Different Partition Key as well as Different Sort Key
- So gives a completely different view of the data
- Speed up any queries realting to this alternative Partition and Sort Key

For example with our user table GSI: Partition Key - email address, Sort Key - last log-in date.

<img src="https://secureservercdn.net/160.153.137.15/3d9.249.myftpupload.com/wp-content/uploads/2017/03/DynamoDB-Secondary-Indexes-GSI-vs-LSI.png">