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

## Concurrent Execution
 * Default is 1000 per region
 * If concurreny > limit, you will see TooManyREquestsException (HTTP status code - 429)
 * **Reserved concurrency** guaranty that a set number of executions which will alaways be available for your critical function.
# DynamoDB

DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit mulliseconds latency at any scale. It is a fully managed database and supports both document and key-value data models. Is is flexible data model and relible performance make it great fit for modbile, web, gamin, ad-tech, IoT applications.

Consistency  models:

 **Eventually Consistent Reads**: Consistancy across all copies of data usually reached within a second. Repeating a read after a short time should return the updated data. (Best Read Performance)

 **Strongly Consistent Reads**: A strongly consistant read returns a result that reflects all writes that received a successful response prior to the read.
 
## DynamoDB - Primary Keys

* DynamoDB stores and retrives data based on a Primary Key 2 types of Primary Key:
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
 - Can only be created when you are creating a table
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

## Query and Scan

**Query** - find items in a table based on the Primary Key attribute and distinct value to search for.

By default a Query returns all the attributes for the items but you can use the **ProjectionExpression** parameter if you want the query to only return the specific attributes you want.

Results are always sorted by Sort Key.Numeric order -by default in ascending. ASCII character code value. You can reverse the order by setting the **ScanIndexForward** parameter.

By default Queries are Eventualy Consistent.You need to explicitly set the query to be Strong Consistent.

**Scan** operation examines every item in the table. By default returns all attribute. Use **ProjectionExpression** parameter to refine the scan to only return the attributes you want.

## DynamoDB Provisioned Throughput

DynamoDB Probisoned Throughput is measured in Capacity Units. When you create table, you specify your requirements in terms of **Read Capacity Units** and **Write Capacity Units**

1 x **Write Capacity Units** = 1 x 1KB write per second
1 x **Read Capacity Units** = 1 x **Strong Consistant Read** of  4KB per second OR 2 x Eventualy Consistent Read of 4KB per second (default)

With **On-Deman** you don't need to specify your requirements (read/write capacity).DynamoDB instantly scales up and down based on the activity of your application.

## DynamoDB Accelerator(or DAX)

**DAX** is fully managed, clustered in-memory cache for DynamoDB.

- DElivers up to a 10x read performance improvement
- Microsecond perfomance for mullions of requests per second
- Ideal for Read-Heavy and brusty workloads.

## Elasticache in front of you DynamoDB

 *  Improve performance of read-heavy worloads
 *  Frequently-accessed data in stored in memory for low-latency access, improving the overall performance of application
 * Good for compute heavy worloads
 * Can be used to store results of I/O intensive database queries or compute-intensive calculations.

 Caching strategies: 

 ***Lazy Loading*** - Loads the data into the cache ony when necessary. If requested data in in the cache, Elasticache returns the data.If the data is not in the cache or has expired, Elasticache returns null.Your application then fetches the data from the database and writes the data received into the cache so that it is available next time

 ***Write Through*** - adds or updates data to the cache whenever data is written to the database.

## Dynamodb transactions

 * ACID Transactions (Atomic, Consistent, Isolated, Durable)
 * Read of write multiple items across multiple tables as an all or nothing operation
 * Check for a pre-requisite condition before writing to a table.

## DynamoDB TTL
  * Time To Live(TTL) attribute defines an expiry time for your data
  * Expired items marked for deletion
  * Greate for removing irrelevant or old data:
    * Session data
    * Event Logs
    * Temporary data
  * Reduces cost by automatically removing data which is no longer relevant.

## DynamoDB Streams

DynamoDB stream - time ordered sequence of item level modifictions (insert, upated, delete). Logs are encrypted at rest and stored for 24 hours. Accessed using a dedicated endpoint.By default the Primary Key is recorded. Before and After iamger can be captured.

Processing DynamoDB Stream:

* Event are recorded in near real-time
* Application can take actions based on contents
* Event sourcing for Lambda
* Lambda polls the DynamoDB stream
* Executes Lambda code based on a DynamoDB Streams event.

# KMS (Key Management Service)

It is a management service that makes it easy for you to create and control the encryption keys used to encrypt your data. AWS KMS is integrated with other AWS services including EBS, S3, Amazone REdshift, Amazone Elsatic Transcoder, Amazone WorkMail, Amazone Relational Database Service(RDS) and other to make it simple to encrypt your data with encryption keys that you manage

**The Customer MasterKey**:
  * alias
  * cereation date
  * description
  * key state
  * key material(either customer provided or AWS provided)
  * Can never be exported

Types of keys
 * **Customer Master Key** is used to decrypt thedata key (envelopr key)
 * **Envelope Key** is used to decrypt the data

# SQL (Simple Queue Service)

It's a web service that gives you access to message queue that can be used to store messages while waiting for a computer to process them. SQS is distributed queue system that ebables web service applications to quick and reliable queue messages that once component in the application generates to be consumed by another component. A queue is a temporary repository for messages that are waiting to be preccesed.

Using SQS yoy can decouple the components of an application so they run independantly, easing message management between components. Any components of a distributed application can store messages in the queue. Messages can contain up to 256KB of text in any format. Any component can later retrive the messages programmatically using the Amazon SQS API.

There are two types of Queue:
 * Standart Queues (default)
 * FIFO Queues (First-In-First-Out)

**Standart Queues** - offers nearly-ultimated numbers of transactions per second.Guaratee that message is delivered at least once. However, occasionally more than one copy of a message might be delivered out of order. Standart queue provide best-effort ordering which ensures that messages are generally delivered in the same order as they are sent.

**FIFO Queues** - complements the standart queue. The most important feature of this queue are FIFO delivery and exactly once processing: The order in which messages are sent and received is strictly preserved and message is delivered once and remains available unitl a consumer processes and delete it; duplicates are not introduced into the queue. FIFO queues also support messages groups that allows multiple ordered messages groups within a single queue. FIFO queues are limited to 300 transactions per secon (TPS), but have all the capabilities of standart queues.

<img src="https://k2y3h8q6.stackpathcdn.com/wp-content/uploads/2018/12/AWS-Training-Amazon-SQS-1.jpg">

https://blog.mailtrap.io/amazon-sqs-tutorial/
https://tutorialsdojo.com/amazon-sqs/

### SQS Delay Queues - postpone delivery of new messages

  * Postpone delivery of new messages to a queue for a number of seconds
  * Messages sent to the **Delay Queue** remain invisible to consumer for duration of the delay period
  * Default delay is 0 seconds  maximu is 900
  * For standart queues, changing the settings does't affect delay of messages already in the queue, only new messages
  * For FIFO queue, this affects the delay of messasages already in the queue

When should you use Delay Queue ?
 - Large distributed applications which may need to introduce a delay in processing
 - You need to apply a delay to an entire queue of messages.
 - e.g adding a delay of a few seconds, to allow for updates to your sales and stack control databases before sending a notification to  a customer confirming an online transaction.

### Managing Large SQS Messages

Best Practice for manage Large SQS Messages Using S3:
 - For large SQS messages 256KB up to 2GB in size
 - Use S3 to store the messages
 - Use Amazone SQS Extended Client Library for Java to manage them

# SNS (Simple Notification Service)

It's make easy to set up, operate and send notifications from the cloud. It Provides developers with a highly scalable, flexible and cost-effective capability to publish messages from an apllication and immediatly delivery them to subscribers or other applications.

SNS allows you to group multiple recipients using topics. A topic is an "access point" for allowing recipients to dynamicly subscribe for identical copies of the same notification.

One topic can support deliveries to multiple endpoints type - for exanple, you can group together IOS, Android and SMS recipients. When you publish once to a topic, SNS delivers message to each subscriber.

# SES (Simple Email Service)

Scalable and highly available email service designed to help marketing teams and application developers send  markering, notification and transactional emails to their customers using a pay as you go model.

Can also be used to receive emails: incomming mails can be delivered automaticaly to an S3 bucket.

Incomming mails can be used to trigger Lambda functions and SNS notifications.

### Difference between SNS and SES

https://www.quora.com/Whats-the-difference-between-Amazon-SNS-and-SES?share=1
https://stackshare.io/stackups/amazon-ses-vs-amazon-sns

### Difference between SNS and SQS

https://dev.to/exampro/sns-vs-sqs-aws-messaging-services-know-the-difference-49p

https://stackoverflow.com/questions/13681213/what-is-the-difference-between-amazon-sns-and-amazon-sqs

# Kinesis

Amazon Kinesis Streams are used to gather together and process huge streams of data records in real-time. Kinesis Data Stream Applications can be created, which are data-processing applications. These applications perform the reading from a data stream in the form of data records. They use Kinesis Client Library for these operations and can run on Amazon EC2 instances. Processed records can be sent to dashboards and can be used to generate alerts, send data to other AWS services, and dynamically change advertising and pricing strategies.

Core Kinesis Services:

 * **Kinesis Streams**
 * **Kinesis Firehose**
 * **Kinesis Analytics**

https://www.sumologic.com/blog/kinesis-streams-vs-firehose/
 

# Elastic Beanstalk

Elastic Beanstalk is a service for deploying and scaling web applications development in many popular languages: JAVA, .NET, PHP, Node.js, Pythone, Ruby, Go and Docker onto widely used application server platforms like Apache Tomcat, Nginx, Passenger and IIS.

Developrs can foucs on writing code and don't need to worry about any of hte underlying infrastructure needed to run the applicaions.

* Faster and simplest way to deplo your application in AWS
* Automaticaly scales your application up and down
* You can select the EC2 instance type that is optimal for your application
* You can retain full administrative control over the resoucer powering your application or have Elastic Beanstalk do it for you
* Manage Platform Updates feature automatically applies ipdates your Operation System, Java, PHP, etc.
* Monitor and manage application health via dashboard
* Integrated with CloudWatch and X-Ray for performance data metric.

## Elastic Beanstalk Deployment Policies

 * All at once
 * Rolling
 * Rolling with additional batch
 * Immutable

**All at once**:
  - Deploys the new version to all instances simultaneously
  - All of your instances are out of service while the deployment takes place.
  - You will experience an outage while deployment is taking place - not ideal for mission-critical production systems
  - If the update fails, you need to roll back the changes by re-deploying the original verison to all your instances.

**Rolling**:
 - Deploys the new verison in batches
 - Each batch of insatnces is taken out service while the deployment takes place.
 - Your envirment capacity will be reduced by the number of instances in a batch while the deployment takes place
 - Not ideal for performance sensetive systems
 - If the update fails, you need perform an additional rolling update to roll back the changes.

**Rolling with additional batch**:
  - Launches an additional batch of instaces
  - Deplys the new version in batches
  - Maintains fully capacity during the deployment process.
  - If the update fails, you need to perform an additional rolling update to roll back the changes.

**Immutable**:
  - Deploys the new version to a fresh group of instances in their own new autoscaling group.
  - When the new instances pass their health checks, they are moved to your existing auto scaling group and finaly the old instances are terminated.
  - Maintains full capacity during the deployment process.
  - The impact of failed updated is far less, and the rollback process requires only terminating the new auto scaling group.
  - Preferred option for Mission Critical production systems.


# CI/CD

CI - continuous integration
CD - continuous Delivery/Deployment

Make small changes & automate everything. Samll, incremental code changes. Automate as possible e.g code integration, build, test and deployment.

https://dev.to/testingnews1/ci-cd-101-all-you-need-to-know-4j04

https://www.infoworld.com/article/3271126/what-is-cicd-continuous-integration-and-continuous-delivery-explained.html

### AWS developer tools:
-  **CodeCommit** - source and version control
-  **CodeBuild** - compiles source code, runs tests and produces packages that are ready to deploy
-  **CodeDeploy** - Automated Deployment to any instance, including EC2, Lambda and on-premises.
-  **CodePipeline** - Manage the workflow, end-to-end solution, build test and deploy your application every time there is a code change.

CI/CD whitepaper - https://d1.awsstatic.com/whitepapers/DevOps/practicing-continuous-integration-continuous-delivery-on-AWS.pdf

# CodeDeploy

CodeDeploy  Deployment Approaches:
 * In-Place - the application is stopped on each instance and the new release is installed. Also known as Rolling Updated.
 * Blue / Green - new instaces are provisioned and the new releases is installed on the new instances. Blue represents the active deployment, green is the new release.

**In-place**
 - Capacity is reduced during the deployment
 - Lambda is not supported
 - Rolling back involves a re-deploy
 - Great when deploying the first time

**Blue/Green**
 - No capacity reduction
 - Green instances can be created ahead of time
 - Easy to switch between old and new.
 - You pay for 2 environments unitl you terminate the old servers.

# CodePipeline

A fully manage CI/CD Service.
 - Orchestrate Build, Test & Deployment. The pipeline is triggered every time there is a change to your code.
 - Automated Realease Process. Fast, consistent, fewer mistakes. Enables quick release of new features and bug fixes.
 - CodePipeline integrates with: CodeComit, CodeDeploy, GitHub, Jenkins, Elastic Beanstalk, CloudFormation, Lambda, Elastic Container Service.

# Elastic Container Service

ECS - a container orchestration service which supports Docker and Windows Containers. Quickly deploy and scale containerized workloads without having to install, configurem manage and scale your own orchestration platform. ECS is built to perform at scale, offers high availability and security, and is deeply integrated with a variety of AWS services, including Elastic Load Balancing, Amazon VPC, AWS IAM, and more. Additionally, Amazon ECS features AWS Fargate, so you can deploy containers without provisioning servers, ultimately reducing management overhead.

 - Cluster of  Virtual Machines. ECS will run your containers on cluster of virtual machines.
 - Farget for Serverless. Use Farget for Serverless containers and you don't need to worry about the underlying EC2 instances !
 - EC2 for more control.If you want to control the installation, configuration and management of your compute environment.

https://d1.awsstatic.com/whitepapers/DevOps/running-containerized-microservices-on-aws.pdf

https://12factor.net/

# CloudForamtion

It's a service that allows you to manage, configure and provision your AWS infrastructure as code. Resources are defined using a CloudFormation template. CloudFormation interprets the template and makes the appropriate API calls to create the resources you have defined. Supports **YAML** and **JSON**.

CloudFormation Benefits:
 - Infrastructure is provisioned consistently, with fewer mistakes.
 - Less time and effort than configuring things manually
 - You can verison control and peer review you templates.
 - Free to use
 - Can be used to manage updates and dependencies
 - Can be used to rollback and delete the entire stack as well


**Resources** is the only mandatory section of the CloudFormation

**Transform** section is used to reference additioonal code stored in S3, allowing for code re-use, e.g for Lambda coder template snippets - reusable pieces of CloudFormation code.

# Web Identity Federation

Web Identity Federation lets you give your users access to AWS resources after they have successfully authenticated with a web-based identity provider like Amazone, Facebook, Google. Following successful auteintication, the user receives an authintication code from the Web ID provider, which they can trade temporary AWS security credentials.

## Amazone Cognito

Amazone Cognito - provides Web Identity Federation with the following features:
 * Sign-up and sign-in to your apps
 * Access for guest users
 * Act as Identity Broker between your application and Web ID providers, so you don't need to write ant additional code
 * Synchronize user data for multiple devies
 * Recommended for all mobile aplications AWS services.

## Cognito User Pools

User Pools - are user directories used to manage sign-up and  sign-in functionality for mobile and web applications. User can sign-in directly to the User Pool or inderictly via an identity provider like Facebook, Amazone or Google. Cognito acts as Identity Broker between the ID provider and AWS. Successful authentication generates a number of JSON Web tokens(JWTs).

Identity Pools - enable you to create unique identites for your users and authinticate them with identity providers. With an identity, toy can obtain temporary, limited-privilege AWS credentials to access other AWS services.


<img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fscriptcrunch.com%2Fwp-content%2Fuploads%2F2016%2F08%2Faws-iam-sts.png&f=1&nofb=1" />

# Advanced IAM Policies

Identity Access Management (IAM) is used to define user access permissions within AWS. There are 3 different types of IAM policies available:
 * Managed Policies
 * Customer Managed Policies
 * Inline Policies

**Managed Policies** - is an IAM policy which is created and administered by AWS. AWS provide Managed Policies for customer use  caseson job function e. ***AmazoneDynamoDBFullAccess***, ***AWSCodeCommitPowerUser***, etc. The AWS-provided policies allow you to assign  apprpriate  permission to your users, groups and roles without having to write the policy yourself.

**Customer Managed Policies** - is a standalone policy that you create and administrate inside your own AWS account. You can attach this policy to multiple users groups and  role - but only within your own account.

**Inline Policies** - is an IAM plicy which is actualy embedded within the user, group or role it applies. There is a strict 1:1 relationship between the entity and policy. When you delete the user/group/role in which the inline policy is embedded the policy will also be deleted.]

### IAM Policy Simulator
  * Test the effects of IAM policies before commiting them to production
  * Validate that the policy works as expected
  * Test policies already attached to existing users - great for troubleshooting an issue which you suspect is IAM related.
# STS (Security Token Service) 

**assume-role-with-web-identity** is an API provide by STS (Security Token Service).Returns temporary security credentials for users authenticated by a mobile or web application using a Web ID provider like Amazone, Facebook, Google, etc. Cognito recommended for mobile applications. Regular web applications can use the STS assume-role-with-web-identity API.

<img src="https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2016/09/24/BrianWagner_stsAssumeRole.png" />

# Cloudwatch 

It's a monitoring service to monitor AWS resources, as well as the applications that you run on AWS.

Cloudwatch can monitor things like:
   * Compute
     * Autoscaling Groups
     * Elastic Load balancers
     * Rout53 Health Checks
    * Storage & Content Delivery
      * EBS Vlumes
      * Storage Gateways
      * CloudFront
    * Database & Analytics
      * DynamoDB
      * Elasticache Nodes
      * RDS Instances
      * Elastic MapReduce Job Flows
      * Redshift
    * Other
      * SNS Topics
      * SQS Queues
      * Opsworks
      * CloudWatch Logs
      * Esimated Charges on your AWS Bill


Host Level Metrics Consists of:
  - CPU
  - Network
  - Disk
  - Status Check

**Exam Tip** : RAM Utilization is a custome metric ! By default EC2 monitoring is 5 minute intervals, unless you enable detailed monitoring which will then make it 1 minute intervals.

You can retrive data using the GetMetricStatistic API or by using third party tools offered by AWS partners. 

You can stroe you log data in CloudWatch Logs for as long as you want. Be default, CloudWatch Logs will store your data indefinitely. You can change the retation for each Log Group at any time.

### Metric Granularity.

It depends on the AWS service. Many default metrics for many default services are 1 minute, but it can be 3 or 5 minute depending on the service.

**Exam Tip** : For custome metrics the minimum granularity that you can have is 1 minute.

### CloudWatch Alarms

You can create an alarm to monitor any Amazon CloudWatch metric in your account. This can include EC2 CPU Utilization, Elastic Load Balancer Latancy or even the charges on your AWS bill. You can set the appropriate thresholds in which to trigger the alarms and also set what actions should be taken if an alarm state is reached.

### CloudWath vs CloudTrail vs Config

* CloudWatch monitors performance
* CloudTrail monitors API calls in the AWS platform
* AWS Config records the state of your AWS environment and can notify you of changes.

# Lambd + VPC

Enabling Lambda to Access VPC Resources
 * To enable this, you need to allow the function to connect to the private subnet.
 * Lambda needs the following VPC Configuration information so that it can connect to the VPC:
  * Private subnet ID
  * Security group Id (with required access)
  * Lambdas uses this infomation to set up ENIs using available IP address from your private subnet.
  