# SAA-C02 Notes
<details>
  <summary>TOC</summary>

- [SAA-C02 Notes](#saa-c02-notes)
  - [AWS Fundamentals: IAM & EC2](#aws-fundamentals-iam--ec2)
    - [Regions](#regions)
    - [IAM](#iam)
      - [Best practices](#best-practices)
      - [Misc IAM](#misc-iam)
      - [SDK](#sdk)
    - [EC2](#ec2)
      - [Instance Metadata Endpoint](#instance-metadata-endpoint)
      - [Security Groups](#security-groups)
      - [Elastic IPs](#elastic-ips)
      - [Instance Launch Types](#instance-launch-types)
        - [Spot Instances Deep Dive](#spot-instances-deep-dive)
      - [Instance Types](#instance-types)
      - [AMIs](#amis)
        - [Elastic Beanstalk](#elastic-beanstalk)
      - [Placement Groups](#placement-groups)
      - [Elastic Network Interfaces (ENI)](#elastic-network-interfaces-eni)
    - [💡 Study](#-study)
  - [High Availability and Scalability: ELB & ASG](#high-availability-and-scalability-elb--asg)
    - [Scalability](#scalability)
    - [Load Balancing](#load-balancing)
      - [Types of AWS Load Balancers](#types-of-aws-load-balancers)
      - [Load Balancer Stickiness](#load-balancer-stickiness)
      - [Cross Zone Load Balancing](#cross-zone-load-balancing)
      - [SSL/TLS Certs](#ssltls-certs)
      - [Connection Draining](#connection-draining)
      - [Auto Scaling Group (ASG)](#auto-scaling-group-asg)
        - [Scaling Policies](#scaling-policies)
        - [Default Termination Policy](#default-termination-policy)
        - [Lifecycle Hooks](#lifecycle-hooks)
        - [Launch Template vs Launch Configuration](#launch-template-vs-launch-configuration)
  - [* recommended = template](#ullirecommended--templateliul)
    - [💡 Study](#-study-1)
  - [EC2 Storage - EBS & EFS](#ec2-storage---ebs--efs)
    - [EBS](#ebs)
    - [EBS Volume Types](#ebs-volume-types)
    - [EBS Snapshots](#ebs-snapshots)
    - [EBS vs Instance Store](#ebs-vs-instance-store)
    - [EBS RAID](#ebs-raid)
    - [EFS](#efs)
  - [* storage tiers: set lifecycle of files, standard, infrequent access (EFS-IA) - pay to access files](#ullistorage-tiers-set-lifecycle-of-files-standard-infrequent-access-efs-ia---pay-to-access-filesliul)
    - [💡 Study](#-study-2)
  - [RDS - Relational Database Service](#rds---relational-database-service)
    - [RDS Read Replicas vs Multi AZ](#rds-read-replicas-vs-multi-az)
      - [RDS Multi AZ](#rds-multi-az)
    - [RDS Security](#rds-security)
      - [Operations](#operations)
      - [Network Security](#network-security)
    - [Aurora](#aurora)
    - [Elasticache](#elasticache)
      - [Redis vs Memcached](#redis-vs-memcached)
      - [Cache security](#cache-security)
      - [Patterns](#patterns)
    - [💡 Study](#-study-3)
  - [Route 53](#route-53)
    - [Records](#records)
      - [TTL](#ttl)
      - [CNAME vs Alias](#cname-vs-alias)
    - [Routing Policies](#routing-policies)
      - [Route 53 Health Checks](#route-53-health-checks)
    - [💡 Study](#-study-4)
  - [AWS S3](#aws-s3)
    - [Versioning](#versioning)
    - [Encryption](#encryption)
      - [Encryption in transit](#encryption-in-transit)
    - [S3 Security](#s3-security)
    - [S3 Bucket Policies](#s3-bucket-policies)
    - [Static Websites](#static-websites)
    - [CORS](#cors)
    - [S3 Consistency Model](#s3-consistency-model)
    - [S3 MFA-Delete](#s3-mfa-delete)
    - [Access Logs](#access-logs)
    - [S3 Replication](#s3-replication)
    - [Storage Classes](#storage-classes)
    - [S3 Lifecycle Policies](#s3-lifecycle-policies)
    - [S3 Performance](#s3-performance)
    - [S3 + Glacier Select](#s3--glacier-select)
    - [Event Notifications](#event-notifications)
    - [Object and Vault Lock](#object-and-vault-lock)
    - [Athena](#athena)
  - [* use case: BI, analytics, analysis, reporting, log analysis](#ulliuse-case-bi-analytics-analysis-reporting-log-analysisliul)
    - [💡 Study](#-study-5)
  - [Cloudfront](#cloudfront)
    - [Cloudfront Signed URL + Cookies](#cloudfront-signed-url--cookies)
    - [Global Accelerator](#global-accelerator)
  - [* acts as a proxy to the application from the edge regardless of the location to minimise latency and provide reliability.](#ulliacts-as-a-proxy-to-the-application-from-the-edge-regardless-of-the-location-to-minimise-latency-and-provide-reliabilityliul)
  - [Storage Extras](#storage-extras)
    - [Snowball](#snowball)
    - [Storage Gateway](#storage-gateway)
    - [FSx](#fsx)
  - [Decoupling Applications](#decoupling-applications)
    - [SQS](#sqs)
      - [Message visibility timeout](#message-visibility-timeout)
      - [Dead Letter Queues (DLQ)](#dead-letter-queues-dlq)
      - [Delay Queue](#delay-queue)
      - [SQS - FIFO Queues](#sqs---fifo-queues)
      - [SQS + Auto Scaling](#sqs--auto-scaling)
    - [SNS](#sns)
      - [SNS + SQS Fan Out Pattern](#sns--sqs-fan-out-pattern)
    - [Kinesis Data Streams](#kinesis-data-streams)
    - [SQS vs SNS vs Kinesis](#sqs-vs-sns-vs-kinesis)
    - [Amazon MQ](#amazon-mq)
  - [* useful for legacy apps that need to be migrated to the cloud without fully reengineering application messaging](#ulliuseful-for-legacy-apps-that-need-to-be-migrated-to-the-cloud-without-fully-reengineering-application-messagingliul)
  - [Serverless](#serverless)
    - [Limits](#limits)
    - [Lambda @ Edge](#lambda--edge)
    - [DynamoDB](#dynamodb)
      - [Advanced Features](#advanced-features)
    - [API Gateways](#api-gateways)
      - [API Gateway Security](#api-gateway-security)
    - [AWS Cognito](#aws-cognito)
    - [Serverless Application Model](#serverless-application-model)
  - [* configured via YAML](#ulliconfigured-via-yamlliul)
  - [Databases](#databases)
    - [Relational Databases](#relational-databases)
    - [Caching](#caching)
    - [NoSQL DBs](#nosql-dbs)
    - [Object Store](#object-store)
    - [Warehousing](#warehousing)
    - [Search](#search)
    - [Graphs](#graphs)
  - [* managed graph database and used for graphing jobs.](#ullimanaged-graph-database-and-used-for-graphing-jobsliul)
  - [Monitoring & Audit](#monitoring--audit)
    - [CloudWatch Metrics](#cloudwatch-metrics)
      - [Dashboards](#dashboards)
    - [CloudWatch Logs](#cloudwatch-logs)
    - [CloudWatch Alarms](#cloudwatch-alarms)
    - [CloudWatch Events](#cloudwatch-events)
    - [CloudTrail](#cloudtrail)
    - [AWS Config](#aws-config)
    - [CloudWatch vs CloudTrail vs AWS Config](#cloudwatch-vs-cloudtrail-vs-aws-config)
    - [💡 Study](#-study-6)
  - [IAM Advanced](#iam-advanced)
    - [Identity Federation](#identity-federation)
    - [Directory Services](#directory-services)
    - [Organisations](#organisations)
    - [IAM Advanced](#iam-advanced-1)
    - [Permission Boundaries](#permission-boundaries)
    - [AWS Resource Access Manager](#aws-resource-access-manager)
    - [AWS SSO](#aws-sso)
  - [AWS Security](#aws-security)
    - [KMS](#kms)
      - [Key Policies](#key-policies)
    - [SSM](#ssm)
    - [Secrets Manager](#secrets-manager)
    - [CloudHSM](#cloudhsm)
    - [Shield](#shield)
    - [DNS](#dns)
  - [AWS Networking](#aws-networking)
    - [NACL / Security Groups](#nacl--security-groups)
    - [VPC Peering Connection](#vpc-peering-connection)
    - [VPC Endpoints](#vpc-endpoints)
    - [VPC Flow Logs](#vpc-flow-logs)
    - [Bastion Host](#bastion-host)
    - [Site to Site VPN](#site-to-site-vpn)
    - [Direct Connect + Gateway](#direct-connect--gateway)
    - [Egress only internet gateway](#egress-only-internet-gateway)
    - [AWS Links](#aws-links)
      - [AWS PrivateLink aka Endpoint Service](#aws-privatelink-aka-endpoint-service)
      - [AWS ClassicLink](#aws-classiclink)
      - [VPN CloudHub](#vpn-cloudhub)
    - [Transit Gateway](#transit-gateway)
    - [Costs](#costs)
  - [Disaster Recovery](#disaster-recovery)
      - [General Tips](#general-tips)
    - [Database Migration Service (DMS)](#database-migration-service-dms)
    - [On premise strategy](#on-premise-strategy)
    - [DataSync](#datasync)
      - [A collapsible section with markdown](#a-collapsible-section-with-markdown)
  - [Heading](#heading)
</details>


## AWS Fundamentals: IAM & EC2

### Regions
* **Regions** = cluster of data centers e.g. US East Ohio (us-east-2).
* most AWS services are region specific.

* **AZ** = Availability Zone.
* discrete data center/s that are connected with each other.
* 1 Region can have multiple AZ e.g. us-east-2a, us-east-2b...

### IAM
* **IAM** = Identity & Access Management.
* Manage **users, groups, roles**.
* Example:
```
User: Jane
Groups: engineering, QA
Roles: attached to internal AWS resources
```

All of the above are set up via policies (JSON; pre-made policies available).

#### Best practices
* One IAM user per person.
* IAM not to be shared or put in code.
* One IAM role per application.
* Use principle of least privilege for security. 
* Do not use the root account after initial setup.

#### Misc IAM

* inline policies can be attached to role but it is not recommended. 
* policies can be assigned to a user, group or role. 
* visual editor or edit JSON
* policy simulator can be used for testing
* policies include an **implicit deny**. You must specify service to grant access. 

#### SDK

* Programming languages have AWS integration via SDK. E.g. Python3 = boto3
* Default region is us-east-1
* Should utilise `~/.aws/credentials`, IAM roles, environment variables
* API is rate limited

### EC2

Some cool new features:
* EC2 hibernation
  * RAM state is preserved
  * RAM written to file and stored on root **encrypted** EBS volume
  * Only some EC2 instances supported <150 GB memory
  * on-demand and reserved only
  * max 60 day hibernation

#### Instance Metadata Endpoint

`http://169.254.169.254/latest/meta-data/`

 * obtain:
   * role name NOT policy
   * but can obtain temp credentials via `.../iam/security-credentials/<iamrole>`

#### Security Groups
* Think of security groups as your firewall config. 
* Controls **ports, ip ranges, inbound and outbound** connections
* Attached to multiple instances
* Region/VPC specific
* Works independently of EC2

#### Elastic IPs
* Own the IP until you delete it.
* Limit: 5 IPs per account

#### Instance Launch Types

1. on demand
  * billing per second after 1st minute
  * good for ad-hoc elastic workloads
2. reserved
  * 1 - 3 years reservation
  * up to 75% discount
  * e.g. database 
  * **subtype**: convertible reserved instance
    * can change instance type
    * discount max ~50%
  * **subtype**: scheduled reserved instance
    * schedule when instance is launched 
    * eg. fractional workload uses
3. spot instances
  * instances lost when a **max price** is reached. 
  * up to 90% discount
  * use cases: batches, data analysis, image processing, non-critical. **Reserved instances** for baseline apps + **on demand** or **spot** for peaks.   
4. dedicated instances
  * shared hardware owned by you
  * other instances (same account) may share this hardware
  * auto instance placement
5. dedicated hosts
  * full control of EC2 instance including sockets + cores + HW
  * min 3 year reservation

##### Spot Instances Deep Dive
* 2 min grace period where instance can be **stopped** or **terminated** when max price is reached.
* **spot block** - reserve for 1-6 hours.
* Request types: a) one-time and b) persistent request
  * one time = the entire spot instance process is stopped
  * persistent = if spot instance is lost, it will continue the spot instance process and assign an instance when available as per your price limits.
* cancellation = remove spot request first and _then_ remove spot instances
* Spot fleet = set of spot instances + (opt) on-demand instances set by definitions
  * lowestPrice - cost
  * diversified - availability
  * capacityOptimized - instance count

#### Instance Types

**R** - RAM - e.g. memcache

**C** - CPU - e.g. compute/db

**M** - balanced - e.g. general/web app

**I** - good I/O - databases

**G** - GPU - video rendering

**T2/T3** - burstable - depletes burst credits

**T2/T3** Unlimited - unlimited bursts

#### AMIs

* **AMI** = Amazon Machine Image
* **Golden AMI** - an EC2 image with everything configured and initiated. This golden image can be used to reduce app loading times. 

##### Elastic Beanstalk

* developer centric view of deploying apps on AWS --> managed service
* free; only pay for instances; only worry about the code.
  * single instance deployment: dev work
  * ALB + ASG: web apps in prod
  * ASG only: non web apps in prod
* supports: go, java, php, packer, docker, etc. 

* **🗺 Region specific**
* Stored in S3 + charged
* default = private to account

**Advantages**:
* pre-installled packages
* satisfy security + compliance
* convenience + efficiency  

**Cross account AMI copy**
* cannot copy AMI with `billingProduct` code e.g. Windows AMI + AWS Marketplace AMI that is shared from **another** account. For this you have to run EC2 with that shared AMI and then copy. 
* if copy rights are not granted, you are still able to create a copy by running EC2 and then create AMI. 
  * usually a shared AMI also needs to give you S3 or EBS access if you want to make a copy. 
* Encrypted AMIs require shared decryption key, running EC2 and then making a copy with your own key. 

#### Placement Groups

1. Cluster
  * all EC2 instances in the same hardware group e.g. same rack + same AZ
  * pros: good network 10gbs
  * cons: if rack fails, no fallback
  * uses: data job, apps requiring low latency + high bandwidth

2. Spread
  * all EC2 located on diff. hardware e.g. diff AZ
  * pros: less chance of failure
  * cons: limited to 7 instances per AZ per placement group
  * uses: HA, critical applications

3. Partition
  * AZ is split into partitions where all EC2s run.
  * 7 partitions / AZ
  * pros: instances do not share rack with other instance partition. Damage controlled to partition vs entire AZ, instances can access metadata
  * cons: many EC2s can be affected if there are not enough partitions
  * uses: HDFS, Kafka, distribution

#### Elastic Network Interfaces (ENI)

* ENI = virtual network card
  * one or more private ipv4
  * one elastic IP per private IP
  * can be moved between EC2
  * AZ bound
  * eth0 cannot be detached

---
### 💡 Study

<details>
  <summary>Security groups can be attached to __ instances</summary>

* **multiple**
</details>

<details>
  <summary>If it's a _timeout_ error then it's a ____ issue. If it's a _connection refused_ error then it's an ____ error.</summary>

1. **security group**
2. **application**
</details>

<details>
  <summary>Security groups by default ____ inbound traffic and _____ outbound traffic</summary>

1. **block**
2. **allow**
</details>

<details>
  <summary>If I stop and then start EC2 instance without using elastic IP, the IP will ____</summary>

* **change**
</details>

<details>
  <summary>User data on EC2 is run with **** rights</summary>

* **sudo**
</details>

<details>
  <summary>Transferring data from ____ to Amazon S3, Amazon Glacier, Amazon DynamoDB, Amazon SES, Amazon SQS, or Amazon SimpleDB in the same AWS Region has no cost at all</summary>

* **EC2**
</details>

<details>
  <summary>AWS provisions max ____ instances per region (req for increase needed)</summary>

* **20**
</details>

<details>
  <summary>A security group is region bound. True or False?</summary>

* **True**
</details>

---

## High Availability and Scalability: ELB & ASG

### Scalability

* **Vertical** = small instance --> large instance e.g. non distributed, databases
* **Horizontal** = 6 x small instances e.g. distributed, web apps
* **High Availability** = run in at least 2 DC (usually paired with hor. scaling)

### Load Balancing

**Load Balancer** = servers that forward internet traffic to multiple servers downstream.
* DNS based
* can be internal or external ELBs
* newer generations recommended
* cannot scale instantaneously. 
* monitoring = cloudwatch metrics + access is logged

**Troubleshooting**:
- 4xx - client errors
- 5xx - app errors
- 503 - over capacity or no target
- Check SGs!

#### Types of AWS Load Balancers
1. Classic load balancer v1: http/s, tcp - CLB
* health check done via HTTP/TCP
* fixed hostname
2. Application load balancer v2: http/s, websocket - ALB
* route based on URL to EC2, ECS, Lambda, private IPs 
* EC2 does not see client IP (only private IPs to ALB). Instead this is done via `X-Forwarded-*`
3. Network load balancer v2: TCP, TLS, UDP = NLB
* route based like ALB
* high performance, low latency
* IP based (per AZ)
* requires inbound TCP rule in SG

#### Load Balancer Stickiness
* ensure same client is directed to same instance behind LB. (1m - 7d)
* Works for CLB and ALB
* performed via a **cookie**
* use case: ensure clients don't lose user data.

#### Cross Zone Load Balancing
* evenly distribute across all instances across all **AZ**s
* CLB = disabled by default, no charge
* ALB = enabled default, no charges
* NLB = disabled by default, $ for AZ transfers

#### SSL/TLS Certs
* allows traffic in transit to be encrypted by client + LB
* issued by CA eg. Lets Encrypt
* Client SSL <--> AWS LB <--> HTTP in private VPC
* managed in AWS cert manager (ACM), X.509 cert. 
* Listener must have a default cert
* Server Name Indication (SNI)
  * allows multiple SSL certs in one server
  * allows hostnames to be distinguish
  * **ALB + NLB only**

#### Connection Draining
* CLB = Connection Draining
* Target Groups = Deregistration Delay (ALB, NLB)
* How long a request should take before sending to the next EC2 instance
  * default = 300s (0-3600 seconds)
* Commonly used to ensure a request can actually complete on an EC2 instance depending on requirements e.g. long = data processing, short = regular web requests 

#### Auto Scaling Group (ASG)
* automation to set minimum, desired, and maximum EC2 instances to match variable loads. 
* work hand in hand with ELB
* scale out = add instances
* scale in = remove instances
* **attributes**:
  * launch config
  * min, max, initial capacity
  * network info
  * load balancer information
  * scaling cooldown = configure buffer between previous and current scaling actions
    * default = 300 seconds, reduce costs with 180 seconds. 
* ASG can be scaled according to CloudWatch alarm + Launch Templates. 
  * e.g average CPU, or network ingress/egress usage
  * custom metrics via application (PUT --> no of connected users)
  * schedule
* **IAM rules attached to ASG attach to EC2 as well**
* ASG is free, just pay for resources launched.
* instances can get terminated+replaced if marked unhealthy by LB

##### Scaling Policies
1. Target Tracking Scaling e.g. 40% CPU averge
2. Simple / Step Scaling e.g. CloudWatch if CPU > 40% then ___ 
3. Scheduled Actions e.g. 10 instances on 5pm Fri

##### Default Termination Policy
* Find AZ with the most instnces
* if multiple instances, choose the one with the oldest launch config. 

##### Lifecycle Hooks
* Keep instances in pending state during ASG actions to perform more actions e.g. scanning, cleaning up. 

##### Launch Template vs Launch Configuration
* Similar
  * Instance metadata settings are pretty much the same
* Differences
  * Launch config == legacy
  * more parameters in templates + spot instances
  * more burst options in template
  * recommended = template
---
### 💡 Study
<details>
  <summary>I cannot use the load balancer *** with multiple SSL certs</summary>
  
* **CLB**
</details>

<details>
  <summary>ALB is Layer * whereas NLB is Layer *</summary>
  
* 7, 4
</details>

<details>
  <summary>NLB provides a ____ IP address</summary>
  
* **static**
</details>

<details>
  <summary>*** can be used for SSL/TLS for multiple domains </summary>
  
* **SNI**
</details>

<details>
  <summary>What happens when an instance fails a health check within ALB? Traffic _______</summary>
  
* **is stopped to the instance immediately**
</details>

---
## EC2 Storage - EBS & EFS

### EBS
* root volume lost when EC2 terminated.
* EBS = elastic block store == **network** drive for persistent data
* re-attachable
* **Bound to AZ**
* Move by snapshotting
* IOPS max at 16000 @ 5TB ~

### EBS Volume Types
* GP2 (ssd)
  * general purpose SSD
  * recommended for dev, test, apps
  * can be made system boot 
  * 1GB - 16TB
  * Like a T2 instance, can burst to 3000 IOPS
* IO1 (ssd)
  * Optimised for IOPS
  * Good for DBs and critical apps. 
  * 4GB - 16TB
  * min 100, max 64000 (nitro) or 32000 IOPS
* ST1 (hdd)
  * streaming workloads e.g. kafka, , logs, data processing/warehouse
  * 500gb - 16tb
  * high throughput
  * **Frequent access**
  * 500 IOPS
* SC1 (hdd)
  * good for low cost, infrequent data
  * cannot be boot volumes
  * 500gb-16tb
  * 250 IOPS / max 250MB ps + burst

### EBS Snapshots
* incremental, only backs up changes, uses IO
* stored in S3 (billed for S3)
* detachment not required but recommended when snapshotting
* can make AMI from snapshot
* max 100,000 snapshots

* can be copied to other regions after snapshots and a new volume can be made from them as well to different AZs. 
* EBS encryption
  * all data at rest encrypted
  * data moving from instance to volume also encrypted in flight
  * snapshots are encrypted
  * volumes created from snapshot also encrypted
  * done automatically (AES-256 via KMS)
  * unencrypted snapshots can be encrypted by using `copy` function -> volume created would also be encrypted as a result. 

### EBS vs Instance Store
Instance store offers:
* block storage just like EBS (eg have file systems on it)
* better performance, high iops
* good for scratch/temporal data
* data survives reboot but **NOT stop or termination**
* can't resize the instance store or easy backups


### EBS RAID
* EBS is already AZ redundant. 
* RAID 0 and 1 most recommended in AWS
  * RAID 0 = split data into multiple volumes = higher performance e.g. IOPS [good for DB, high IOPS that doesn't need redundancy] 
* RAID 1 = mirroring = data from EC2 is written to multiple volumes. IOPS remain the same and do not increase like RAID 0. 

### EFS

* Elastic File System
* Network file system; auto scaling FS
* **Can work across AZ**
* 3x more expensive
* only pay for data stored unlike EBS
* EFS is usually behind a security group that is then linked to multiple EC2 instances
* good for: content management, wordpress, standard NFSv4 req.
* **Only for linux AMI**
* encryption = KMS

* performance = 10gbits throughput, can scale up to petabyteS, 1000s of concurrent connections
* performance mode need to be set: gen purpose, max I/0
* storage tiers: set lifecycle of files, standard, infrequent access (EFS-IA) - pay to access files
---
### 💡 Study

<details>
  <summary>What is the difference between EBS and instance store?</summary>

* **instance store is physically attached to the instance instead of a regular root EBS volume**  

</details>

<details>
  <summary>RAID 0 is for ___ and RAID 1 is for _____ ______</summary>

* **performance, fault tolerance**  

</details>

<details>
  <summary>EFS can work across ____</summary>

* **AZs** 

</details>

<details>
  <summary>T / F - Root EBS volumes for EC2 instances get terminated by default if EC2 is terminated</summary>

* **True** - the behaviour can be changed during setup though.  

</details>

<details>
  <summary>T / F - You can only attach 1 IAM role to an EC2 instance</summary>

* **True**  

</details>

---
## RDS - Relational Database Service
* managed DB with SQL support
* multiple databases supported e.g. postgres (TDE), msql, mariadb, oracle, microsoft sql, aurora (aws)
* pros:
  * managed (can't SSH into RDS)
  * continuous backups
  * monitoring
  * multi az; ebs
  * better performance + scaling vertical and horizontal. 
* auto backups **daily** and every 5 mins
* 7-35 days retention
* **snapshots** available manually

### RDS Read Replicas vs Multi AZ

* upto 5 read replicas can be made AZ, cross-AZ, cross-region
* async replication (eventually consistent)
* replicas can be made their own DBs as well
* **read only**
* **use case**: create read replicas to support new apps that need the DB
* network cost occurs if RDS -> RR (diff AZ) for the replication. Doesn't occur if RDS + RR is in same AZ. 

#### RDS Multi AZ
* Master RDS -> SYNC replication 
* replicated to diff AZ (**standby instance**)
* auto failover via dns name
* read replicas can also be set up as multi AZ. 


### RDS Security
* at rest 
  * master and read replicas can be encrypted (KMS AES 256)
  * must be done when launching
  * if master != encrypted, read replicas cannot be encrypted either. 
  * alternative: transparent data encryption [only for PSQL]
  
* in flight
  * while data is being sent to the db
  * SSL cert
  * needs to be enforced in certain database apps to force using SSL

#### Operations
* To encrypt an unencrypted RDS database:
  * create snapshot
  * **copy** snapshot and enable encryption
  * restore the db from encrypted snapshot
  * delete old database after migration

#### Network Security
* place in private VPC/subnet
* utilise security groups and IPs to limit access
* use IAM to control RDS management via API
* username/passwd auth for db access
* IAM can be used for auth in db for postgres and mysql -> **via auth tokens (15 mins)**

### Aurora

* compatible with psql and msql
* cloud optimised (3-5x)
* starts at 10gb, can grows to 64TB
* max 15 read replicas
* costs more than RDS but more efficiency

* stores 6 copies across 3 AZs
  * 4 copies for writes
  * 3 copies for reads
  * peer to peer; self healing; replication/striped
* can also do cross region replication (not default)
* dns endpoint for writer
* dns reader endpoint - **connects automatically to read replicas for load balancing**

* writes written to master db
* if it fails, fallback in 30 seconds
* **security**
  * similar to RDS; KMS encryption
  * all backups, snapshots, replicas encrypted

* **serverless**
  * good for infrequent or unpredictable workload
  * pay per second
  * auto db creation and scaling

* **global aurora**
  * cross region read replicas - good for disaster recovery
  * global database
    * 1 primary region (rw)
    * 5 secondary regions
    * 16 read replicas per region


### Elasticache
* managed service of  Redis or Memcached
* help reduce load from databases
* stored in memory
* helps take load off DB reads. 
* useful to write session data to be used across multiple apps
* **Multi AZ failover capability**

#### Redis vs Memcached
* Redis
  * multi AZ possible
  * read replicas available
  * has backup and restore features (primary, replica)

* Memcached
  * sharding multi node
  * non persistent
  * no backup + restore


#### Cache security
* redis
  * support SSL 
  * **do not support IAM** for auth
  * redis AUTH available
* memcached
  * SASL auth

#### Patterns
* lazy loading - all read data in cache - data can become stale; data not in cache accessed from db
* write through - add or update data in cache when written to DB
* session store - store temp data in a cache with TTL features

---
### 💡 Study

<details>
  <summary>Must know DB ports</summary>
    
    PostgreSQL: 5432

    MySQL: 3306

    Oracle RDS: 1521

    MSSQL Server: 1433

    MariaDB: 3306 (same as MySQL)

    Aurora: 5432 (if PostgreSQL compatible) or 3306 (if MySQL compatible)
</details>

<details>
  <summary>What do I need to enable in RDS to ensure IAM authentication can occur?</summary>

* RDS --> IAM DB Authentication (psql and msql only)
</details>

---

## Route 53
* managed DNS service
* used on public or private domains (.com vs .internal)
* $0.50 per month per zone
* also a registrar for domains but 3rd party also possible
  * need to create hosted zone + NS records if 3rd party

### Records

#### TTL
* set a value of how long DNS is cached on client. 
* high = 24hr (lower r53 queries), low = 60s (higher r53 traffic)
* mandatory setting

#### CNAME vs Alias
* AWS resources sometimes provide a AWS DNS hostname e.g. cloudfront
* CNAME = hostname -> hostname/ip *eg only for non root / sub domain e.g. sub.domain.com*
  * paid
* ALIAS = hostname -> aws resource *works for both root/non-root e.g. myname.com -> app234.aws.com*
  * free, recommended
* A record = can have multiple values (IPs only)

### Routing Policies

* **Simple**
  * when you redirect to a single resource e.g. domain -> IP
  * multiple values can also be set but **client decides** how it is chosen

* **Weighted**
  * Control no of % that go to a specific endpoint e.g 10% to IP1, 90% to IP2
  * Useful for split traffic and testing new endpoints

* **Latency**
  * Redirect to server that has the least latency to the client
  * this is in terms of AWS regions closest to the user

* **Failover**
  * needs a R53 health check on primary record
  * when that fails health check, it will be routed to the secondary record. 

* **Geolocation**
  * based on user location and _not_ latency

* **Multi Value**
  * enhanced simple routing that includes health checks
  * not a substitute for ELB

#### Route 53 Health Checks
* unhealthy = 3+ health checks fails
* healthy = 3+ health checks pass
* 30s interval; one request per 2 seconds avg. 
* http, tcp, https (no ssl)




---
### 💡 Study

<details>
  <summary>CNAME only works for *** **** domains</summary>

* **non root**
</details>

<details>
  <summary>Out of CNAME and ALIAS what is paid and free?</summary>
  
* **CNAME is paid, ALIAS is free**
</details>

---

## AWS S3

* prefix + object name
* storage represented as objects that have a key
* tied to region
* unique bucket name (globally) 
* max object size = 5TB
* max object upload = 5GB, more needs to be done via multipart
* metadata (key + value pairs) + tags (max 10) available
* version ID


### Versioning

* versioning - available option
* if you suspend, previous versions are not removed
* versioning allows you to have copies of files as they are updated
* seen via version id
* delete marker prevents unintended deletes. To reverse this delete, just remove the delete marker

### Encryption

1. SSE-S3

* object encrypted by AWS server side (S3 master key)
* AES-256
* header = `AES256`

2. SSE-KMS

* handled and managed by KMS service
* provides key management and auditing
* object encrypted server side via customer master key (CMK)
* header = `aws:kms`

3. SSE-C

* server side encryption
* key managed by customer outside AWS
* only HTTPS
* encryption key in HTTP header

4. Client side encryption

* e.g. S3 encryption client
* encryption performed outside S3 (encrypt before on client, decrypt after)

#### Encryption in transit

* S3 gives HTTP and HTTPS (encryption in flight); HTTPS endpoint recommended

### S3 Security

* user based
  * IAM policies
  * IAM principal can access via user perm -> resource policy ALLOW -> no EXPLICIT DENY
* resource based
  * bucket policies
  * object ACL - fine grain
  * bucket ACL - rare
* block public access is available via settings
* S3 can be accessed via VPC through endpoints
* access logs can be stored on S3 bucket
* API calls sent to Cloudtrail
* MFA delete
* Pre-signed URLs - file valid only for a limited time. 
* **Default encryption** option ensures non-encrypted requests are not accepted. However, bucket policies will be evaluated first. 

### S3 Bucket Policies

* JSON policies
  * resources
  * actions
  * effect
  * principal

* bucket policies are used for fine grain and forced encryption or grant others access. 

### Static Websites
* bucketname.s3-website.region...
* public access needed
* modify the bucket policy

### CORS

* origin = scheme (protocol), host (domain) and port. 
* CORS = cross origin resource sharing
* CORS is a mechanism used to allow requests to other origins when visiting main origin. 
* if you go www.abc.def --> other.website then CORS needs to be enabled on the second server
* if CORS policy is valid, then the client will contact the second server to fetch resource from second server whilst fulfilling the request from the first server. 
  * common use case: bucket-html, bucket-assets == bucket-assets will need CORS set up for bucket-html to fetch assets from buckets-assets. 

### S3 Consistency Model

* servers in region will replicate data (via **eventual consistency**)
* you need to upload and then view
* if you view and then upload it may not be instantly consistent
* GET after PUT, we could still get the older version
* may be able to GET after DELETE

### S3 MFA-Delete

* Only root account can enable MFA delete
* works via CLI only
* Versioning must be enabled -> MFA is only req for delete or suspending versioning

### Access Logs

* set a separate logging bucket

### S3 Replication

* _versioning must be enabled_
* **cross region replication** e.g. compliance, low latency access, copied across accounts
* **same region replication** e.g. log aggregation, replication between prod and test
* async copy
* IAM role needed
* only new files replicated after enabling
* DELETE is not replicated
* no replication chaining e.g. bucket 1 -> 2 -> 3

### Storage Classes

* **General Purpose**
  * **Standard-Infrequent Access** (IA)
    * data that is less frequently accessed
    * less availability than GP
    * good for: data store backups, disaster recovery
  * **One Zone-Infrequent Access** (IA)
    * stored in a single AZ
    * less availability
    * good for: secondary backup, data that can be recreated eg thumbnails
  * **Intelligent Tiering**
    * auto move object across access tiers
    * AZ resistant 
    * tiering fee

* **Glacier**
  * long term data storage for archive/backup
  * item in Glacier = **archive** (upto 40 tb)
  * archives are stored in **vaults**
  * minimum storage duration = **90 days**
  * **Retrieval options**
    * expedited - 1-5m
    * standard - 3-5h
    * bulk - 5-12h
  * **Glacier Deep Archive** - longer term storage
    * retrieval: standard (12h) and bulk (48h)
    * minimum storage = **180 days**

### S3 Lifecycle Policies

* Lifecycle configuration can be set up to automate movement of S3 objects between different storage tiers. 
* rules can be created for: prefix and object tags

* Transition Actions
  * move to snandard IA after 60 days
  * move to glacier after 6 months

* Expiration Actions:
  * set objects to delete after some time e.g. old files, versions, incomplete files. 

### S3 Performance

* auto scaling to latency 100-200ms
* 3500-5500 requests oer second per prefix
* prefix = folder after bucket://...
* KMS encryption impacts performance; quotas are enforced depending on region
* multi part upload recommended for files >100 mb but must be used for >5gb
* **upload** - transfer acceleration via edge locations -> S3; compatible via multipart
* **byte range fetches** - parallel GET via byte ranged; good for resiliency; can also retrieve partial data

### S3 + Glacier Select

* retrieve less data via server side filtering via **SQL**
* data and column selection; faster and cheaper. 

### Event Notifications

* create notifications based on S3 event types and file types
* can be fed to SNS, SQS, or Lambda e.g. thumbnails of all S3 image uploads
* **versioning should be enabled** for best results

### Object and Vault Lock

* S3 Object Lock
  * write once read many (WORM) model
  * block object from deletion 
* Glacier Vault Lock
  * write once read many (WORM) model
  * lock for no further edits

### Athena

* serverless file for S3 analytics
* SQL or other BI tools + JSON CSV etc
* charged per query
* use case: BI, analytics, analysis, reporting, log analysis
---
### 💡 Study

<details>
  <summary>What is the maximum object size for S3?</summary>

* **5TB**

</details>

<details>
  <summary>What is the upload limit size for S3 per segment?</summary>

* **5GB**

</details>

<details>
  <summary>At least how many AZs do S3 objects get stored in (apart from one-zone IA)?</summary>

* **>=3 AZs**

</details>

---

## Cloudfront

* content delivery network = CDN
* good for static content needed all across the world with short lifespan
* also works for dynamic content
* improves read performance due to edge locations (points of presence)
  * sometimes content fetched from edge locations
* origin examples
  * s3 bucket - used for ingress, distributing, security
  * custom origin (http) - alb, ec2, s3 website, etc
* security
  * done via OAI for S3
  * for EC2 or ALB - security group must allow edge public IPs

* geo restrict
  * allowlist and blocklist depending on location

### Cloudfront Signed URL + Cookies

* good for distributing paid and restricted content.
* signed url = individual file access
* signed cookies = multiple file access
* cloudfront signed url is usually more flexible than S3 presigned object urls

### Global Accelerator

* allows faster global access regardless of hosted region
* **unicast IP** = one server = one ip
* **multicast IP** = all servers = same ip ; routed to nearest one
* Global Accelerator uses Anycast IP system leverage the AWS network with **2 ext. IPs** 
* **works with**: elastic ip, ec2, alb, nlp, public or private
* works for a range of apps over TCP and UDP 
* acts as a proxy to the application from the edge regardless of the location to minimise latency and provide reliability. 
---
## Storage Extras

### Snowball

* physical data transport for TB or PB of data to AWS -> copies to S3 only
* 256 KMS encryption
* use case: data migrations, disaster recovery
* if it takes more than a week to transfer data, use snowball. 
* **snowball edge**
  * add compute - add custom EC2 and lambda and perform data processing. good for iot capture, machine learning. 

### Storage Gateway

bridge on prem storage with AWS storage (via virtualisation)

* file gateway - s3 buckets accessed using NFS or SMB
  * recent data cached in gateway
  * **hardware appliance** can also be purchased instead of virtualising yourself for a gateway
* volume gateway - S3 accessed via iSCSI block storage
  * EBS snapshots
  * cached volumes and stored volumes
* tape gateway - s3 or glacier -> virtual tape library (VTL)

### FSx

* EFS is for linux only. FSx is for windows. 
* SMB and NTFS and Active Directory integration
* SSD, 10gb/s, 100PBs of data
* daily backups to S3
* Amazon FSx for Luster (Linux Cluster)
  * different to windows. Used for parallel file systems (large scale computing) -- HPC, ML
  * s3 integration

---

## Decoupling Applications

* allows AWS apps to communicate between each other
* either synchronous [app to app] or async [app to queue to app]
* sync - susceptible to spikes of message volumes
* async fixes the above

### SQS
> simple queue service

* standard queues; application decoupling
* producer (sends message) -> SQS Queue -> messages polled -> consumer/s
  * **producers** send messages via API/SDK e.g. orders
  * message stays there until deleted
  * **consumers** usually run on servers like EC2 or Lambda
  * consumer polls, 10 messages at a time, which is then processed eg insert into RDS
  * can have multiple consumers processed in parallel
  * cloudwatch alarm for queue length can be set to auto scale EC2 that have SQS consumers
* unlimited throughput and amount of messages. 
* min 4 days - max 14 days; 256kb per message
* **security**
  * https in flight
  * kms at rest
  * client side also possible
  * access: IAM & SQS access policies

#### Message visibility timeout

* Visibility timeout prevents the message from being processed for X seconds after first `ReceiveMessage`
* Visibility timeout - Default = 30 seconds
* if more time is needed the consumer will issue `ChangeMessageVisibility`  

#### Dead Letter Queues (DLQ)

* limit can be set to how many times a messages goes back into the queue if not processed within visibility timeout
* Set `MaximumReceives` after which message is sent to DLQ
* useful for debugging; need to retain messages for X days


#### Delay Queue

* prevent seeing the messages immediately in the queue
* default = 0 seconds
* `DelaySeconds` parameter

#### SQS - FIFO Queues

* first in, first out
* more ordered than standard SQS queue
* decoupling & deduping but maintains ordering of messages as they are sent.

#### SQS + Auto Scaling

* scale EC2 instances when messages go above a certain threshold. 
* needs cloudwatch custom metric (queue length / num of instances) and an alarm for that metric

### SNS
> simple notification service

* send messages to many receivers
* producer sends to one SNS topic
* all subscriber gets all messages sent to topic
* subscribers: SQS, HTTP/S, Lambda, Email, SMS, Push
* uses: cloudwatch, S3 bucket events, cloudformation changes
* create topic -> create sub/s -> public topic
* **security**
  * in flight by default
  * at rest via KMS
  * client side encryption
  * access: IAM, SNS access policies

#### SNS + SQS Fan Out Pattern

* SQS queues are connected to SNS topics 
* send once, multiple receives
* **SNS cannot send messages to SQS FIFO queues**

### Kinesis Data Streams

* alternative to Kafka; allows quick data onboarding
* real time big data e.g. logs, IoT - stream processing
* 3 AZ replication
* `PutRecord` + partition key -> allows sequencing and sending to specific shards
* key needs to be distributed so data gets sent to multiple shards e.g. `user_id` as the key. 
* **Kinesis Streams** - streaming ingest at scale
  * shards used to expand data throughput (1mb/s write, 2mb/s read)
  * records are ordered within shards
  * 1-7 day retention
  * data is immutable - can't be deleted
* **Kinesis Analytics**
  * take data from streams or firehose and perform analytics via SQL queries
* **Kinesis Firehose**
  * loads data into redshift, s3, elasticsearch, splunk
  * near real time
  * vs **streams** - serverless data transformation, NOT real time, and doesn't do storage like streams does
* security
  * IAM for access
  * HTTPS for in flight; KMS for at rest
  * client side encryption + VPC endpoints

### SQS vs SNS vs Kinesis

### Amazon MQ

* managed apache Active**MQ**
* queue and topic
* useful for legacy apps that need to be migrated to the cloud without fully reengineering application messaging
---

<details>
  <summary>Maximum days messages stored in SQS standard queue?</summary>
  
* **14 days**
</details>

<details>
  <summary>If I need a lot of consumers for the data that I ingest in a queue, should I use Kinesis or SQS FIFO?</summary>
  
* **SQS FIFO because many consumers can be made according to group ID vs no of shards for Kinesis**
</details>

---
## Serverless

* Serverless == _function as a service_ --> not having to manage a server
* max exec time for serverless = 15 minutes
* more RAM = more network + CPU
* eg thumbnail generator after s3 put, serverless cron jobs

### Limits

* 128mb - 3gb
* max time exec = 15mins
* env variables = 4kb
* 1000 concurrent
* function size = 50mb zipped / 250mb unzipped (use `/tmp` instead)

### Lambda @ Edge

* perform lambda at edge with cloudfront
* we can modify: viewer request, origin request, origin response, viewer response
* use cases: SEO, A/B testing, analytics, dynamic at edge

### DynamoDB

* fast, scalable, managed DB replicated over 3 AZ
* NoSQL based (non-relational) 
  * table + primary key
  * infinite rows
  * each row/item has attributes; max size 400kb
* IAM integrated
* must provision read and write capacity
  * read capacity unit (RCU)
  * write capacity unit (WCU)

#### Advanced Features

* DynamoDB Accelerator (DAX)
  * cache - goes from DAX -> DynamoDB
  * relieved read pressure e.g. 5 minutes TTL cache
  * multi az
* Streams
  * store changes to DDB which can be read by other services eg Lambda [24h retention]
* Transactions
  * all or nothing operations
* On Demand
  * do WCU RCU needed
  * 2.5x more expensive
* Backup & Security
  * IAM + encryption at rest + transit + VPC endpoints
  * DMS as migration service
* Global tables
  * cross region replication (CRUD)
  * needs DDB streams enabled

### API Gateways

* API gateway (lives in 1 region) creates REST public APIs that clients can use to communicate with lambda function
* can be used for lambda, http, and aws service eg SQS
* endpoint types
  * edge optimized - routed via cloudfront edge
  * regional - where clients are in the same region/s or via customer cloudfront
  * private - only access API via VPC endpoint with resource policy defined

#### API Gateway Security

* IAM Permissions
  * Sig v4 needed
  * IAM policy, attached to user or role which the API Gateway can check
* Lambda Authorizer
  * Use Lambda to verify token in header
  * useful with OAuth or SAML
  * tied to IAM
* Cognito user pools
  * user lifecycle management via user pool e.g. fb or google login
  * only does auth and not authorization

### AWS Cognito

* **Cognito User pools** - sign in functionality to use with API gateway
  * serverless database of users
  * federated identities e.g. google, saml
  * sent as JWT
* **Cognito Identity pools** - AWS creds to access AWS resources
  * can be integrated with user pools
  * straight access without API
  * uses federated identity provider
  * gives temp IAM access to resource
* **Cognito Sync** - sync from device to Cognito
  * stores config
  * cross device + offline
  * needs cognito federated identity pools

### Serverless Application Model

* framework to deploy serverless applications
* configured via YAML
---

## Databases

Things to consider for choosing DBs in AWS:
* read or write heavy
* throughput needs?
* scale needs?
* storage size
* durability
* latency
* data model
* schema vs flexibility
* licence costs

### Relational Databases

> good for joins, websites, normalised data

* **RDS**
  * managed DB e.g. PSQL, MSQL
  * EC2 + EBS req. 
  * Read replicas + Multi AZ
  * IAM, KMS, SSL
  * Backups + Snapshots + Scheduled maintenance
  * Monitor via Cloudwatch
* **Aurora**
  * PSQL, MSQL
  * auto healing and scaling 
  * optimised for latency + performance + less maintenance
  * also provides serverless

### Caching
* **Elasticache**
  * key value store - managed memcached/redis
  * not a database!
  * great performance + latency, reliable due to multi AZ + sharding
  * requires EC2
  * NO IAM

### NoSQL DBs

* no joins or SQL. Different data organisation
* **DynamoDB**
  * serverless + IAM + streaming capability
  * also does key value store
  * read and write units are decoupled
  * accelerator = DAX = read cache

### Object Store

* good for backups and big objects
* **S3**
  * good for large objects (up to 5tb)
  * infinite scaling

### Warehousing

* good for analytics + BI
* **Athena**
  * serverless query engine fed from S3
  * IAM + S3
  * analytics, light queries, one time queries for S3

* **Redshift**
  * provides analytics + data warehousing (not transactions) based on psql
  * high performance compared to others 

### Search

* good for unstructured free text search
* **Elasticsearch**
  * used with other databases to do free form searching and partial searches

### Graphs

* **Neptune**
  * managed graph database and used for graphing jobs.
---

## Monitoring & Audit

### CloudWatch Metrics

* available for every _AWS_ service
* metric = variable e.g. cpu, storage
* dimension = attribute of metric e.g. instanceId, environment
  * 10 dimensions per metric
* detailed metric (every **1 minute**) available at a cost
* custom metrics also possible from 1 min to **1 sec** interval

#### Dashboards

* global
* graphs can be included from different regions
* auto refresh available

### CloudWatch Logs

* most AWS services can send logs directly
* other apps need to use SDK
* **Structure**
  * Log groups = represents an application e.g /var/log/messages
  * Log stream = instances, individual log files, containers 
* encryption available KMS etc.
* **Agent**
  * can be installed on on prem or EC2 to forward logs to CloudWatch logs
  * CloudWatch Unified Agent is the newer version and provides more info e.g. cpu, ram, netstat

### CloudWatch Alarms

* trigger notifications from metrics
* go to ASG, EC2 actions, SNS
* States: **OK, INSUFFICIENT_DATA, ALARM**
* **EC2 Instance Recovery**
  * status check = VM or baremetal check
  * CloudWatch can be used to check if EC2 statusCheck is up/down --> set up **EC2 Instance Recovery** if alarm fired to preserve IPs, metadata, groups etc. 
* Period = 10 seconds or 30 seconds

### CloudWatch Events

* cron jobs or event patterns (eg code pipeline pattern)
* trigger to lambda, SNS, EC2 etc
* results in JSON files

### CloudTrail

* enabled by default
* history of events, APIs within AWS account
* includes console, CLI actions
* useful for resources deleted = look in cloudtrail first!

### AWS Config
* record configs and changes over time
* e.g. what buckets are public, what EC2 have SSH access
* per region service but can have global view
* works with SNS 
* custom rules via Lambda
* can chain with CloudWatch Events + auto remediation
* **cannot deny actions - only reacts to changes**

### CloudWatch vs CloudTrail vs AWS Config

* cloudwatch = performance, monitoring, alerting, log aggregation
* cloudtrail = record api calls, audit
* config = record config changes, evaluate resources and get timeline of complaince

### 💡 Study
<details>
  <summary>Cloudwatch Dashboards are available globally and work cross region. True or False?</summary>

* **True**  
</details> 

## IAM Advanced

* security token service - STS
  * valid for 1 hour
  * grants temp access to resources
  * `AssumeRole` - own account or target account  
  * `GetSessionToken` for MFA
* How to assume a role
  * Define IAM role
  * Define principals that can access this role
  * STS to retrieve creds and impersonate the IAM role that you have access to
  * 15m - 1 hour credential life

### Identity Federation

* user outside AWS to assume temp role to access AWS resources
* **SAML 2.0**
  * access to AWS console and resources via identities
  * IAM user for each employee not needed  
  * Active directory also possible and we get temp creds via STS
  * if SAML 2.0 is not compatible with ID provider, a customer app needs to be created that talks to STS
* **Web Identity Federation**
  * not recommended by AWS
  * this is for users outside an org / directory service
* **Cognito**
  * recommended
  * allows using services like fb, google, amazon login to provide AWS access
  * pre defined IAM role attached to authenticated or anonymous users

### Directory Services

* AD = centralised db of objects, users, computers, printers etc. 
  * objects = trees
  * group of trees = forest
* **AWS managed MS AD**  
  * supports MFA
  * can be linked via trusts to on prem AD
* **AD Connector**
  * proxy redirect to on prem AD. All management done on-prem
* **Simple AD**
  * AD compatiable but can't be connected to MS AD
  * Lives on AWS only

### Organisations
* global service
* main account + member accounts
* consolidated billing and benefits

* **Multi Accounts** 
  * accounts per dept, cost center, dev/test/prod, seperate VPCs, seperate logging
* **OU** = organisational units
  * can be split by business units, environments units, or project based. Examples include Sales OU, Prod OU, Project 1 OU
* **SCP** - service control policies 
  * allow and block IAM actions inherited from level above or added at the next level.
  * done at the OU or Account level
  * explicit allow - deny takes precedence
  * does not apply to master account
* **Moving accounts between orgs**
  * From Org A -> Org B, remove the member account first from Org A and then send invite to join Org B
  * For master accounts, remove all accounts below master from Org A, then delete the Org A, invite master user to Org B

### IAM Advanced

* **IAM Conditions**
  * `aws:SourceIP` - can be used for restricting client IP access
  * `aws:RequestedRegion` - restrict region where the requests are made **to**
  * tag based, mfa based
* Resource based policies vs IAM roles
  * Roles give up permissions. So if you need to go from A -> B and then back to A then you may face issues
  * As a result, resource based policies could be better for S3, SNS, SQS
* IAM for S3
  * List related permissions don't need the trailing `*` whereas Get, Put, Delete need :::test/`*` wildcard at the end. 
  * i.e. bucket level vs object level permission

### Permission Boundaries

* permission boundary, when set, can restrict IAM permissions
* e.g. if bounday for IAM is only EC2 and S3 then giving permission to create DynamoDB it will not work. 
* good for providing some privs to non admins, users, or restricting specific users from NOT doing something

### AWS Resource Access Manager

* share resources to other accounts or organisations
* e.g. VPC subnets, transit gateway, route53

### AWS SSO

* manage sign on to 3rd party apps and multiple accounts
* supports SAML + AD
* vs AssumeRoleWithSAML -- AWS SSO doesn't need a seperate setup for each and every service and we don't need to create a login portal seperately. 

---
## AWS Security

### KMS

* Region bound
* KMS handles most encryption within AWS
* **Customer Master Keys (CMK)** - 2 types:
  * Symmetric AES256
  * Asymmetric RSA/ECC e.g public and private keys
  * Default CMK is free (starts with `aws/<service>` alias). User keys are $1 / month + API calls charged
* When is KMS used?
  * when sharing sensitive content, use CMK via API so sensitive data is not stored unencrypted. 
* **KMS Data limit** = 4kB
* Access
  * IAM + Key policies needed

#### Key Policies

* need to be specified to allow access
* define users, roles that can access key and then give IAM roles to users/groups

### SSM

* Systems Manager Agent
* stores configs and secrets
* integrates with CloudWatch + IAM
* can create policies to expire parameters

### Secrets Manager

* allows storing secrets (using KMS) and rotating secrets with auto generation
* integrates with RDS 

### CloudHSM

* alternative to KMS if you want to control the secrets
* Harware Security Module
* AWS cannot retreive keys
* Can be Multi AZ
* Use cloudHSM client software
* works with Redshift, SSE-C

### Shield

* standard is free, protects common attacks
* advanced has DDOS mitigation service and sophistacated attacks

### DNS

* DNS resolution and hostname needs to be enabled for R53 private zones

## AWS Networking

### NACL / Security Groups

* Security group = stateful [instance]
* NACL = stateless [subnet]
* NACLs will evaulate both inbound and outbound individually
* Security groups will auto grant inbound if outbound is allowed for example. 
* NACL
  * one NACL per subnet
  * rules assigned a number - higher number = lower priority
  * will have a default rule of denying everything
  * **use case:** block specific IP within subnets
  * auto applied to instances in the associated subnet (SG not auto applied)

### VPC Peering Connection

* connect 2 VPC together; cross-region, cross-account
* ensure that subnets do not overlap
* each VPC connection needs peering. E.g. A->B->C == A cannot talk to C automatically
* each VPC's subnets route tables need to be updated

### VPC Endpoints

* Access AWS services via private VPC networks
* remove the need for NAT, IGW, etc to AWS services
* common issues: DNS + Route table not configured 
* types: interface & gateway endpoints
* DNS resolution needs to be enabled in VPC for DNS
* Note: in CLI, ensure you use the correct region when calling endpoints (default is us-east in CLI)

### VPC Flow Logs

* logs ip information via interfaces
  * vpc flow logs
  * subnet flow logs
  * ENI flow logs
* go to cloudwatch or S3
* syntax
  * srcaddr, dstaddr - good for network troubleshooting
  * srcport, dstport - good for network troubleshooting
  * Action = success of failure of request
* One way to analyse VPC flow logs is to use Athena (+ S3)

### Bastion Host

* Use this public host to SSH into private instances
* set up in public subnet
* best to restrict port 22 from your IP

### Site to Site VPN

* need to set up customer gateway on offsite DC
* then set up VPN gateway on VPC + site to site connection
* AWS services:
  * Customer Gateway
  * Virtual Private Gateway
  * VPN Connection
* Customer side:
  * IP on cust device needs to be static public IP
  * if behind NAT, use public NAT IP

### Direct Connect + Gateway

* provides direct private connection between remote net to VPC
* ipv4 + ipv6
* virtual private gateway needed
* needed when more b/width is needed or more network stability
* if multi VPC access is needed use a **direct connect gateway**

* connections are not encrypted in direct connect
* direct connect + VPN is available

### Egress only internet gateway

* Only works for IPv6
* similar to IPv4 NAT gateway
* needed as all ipv6 are public

### AWS Links

#### AWS PrivateLink aka Endpoint Service
* a good way to expose your VPC to other external VPCs
* network load balancer + corresponding ENI on customer VPC
* can be multi AZ

#### AWS ClassicLink
* needed for legacy EC2 Classic instances to be linked to VPC

#### VPN CloudHub

* allows to create secure comms between multiple VPN sites. 

### Transit Gateway

* star topology connection between all your VPCs
* regional or cross region
* can be shared across accounts using resource access manager (RAM)
* transit gateways can be peered across regions
* **IP Multicast** supported (_this is the only AWS service that uses this_)
* attach VPC, VPN, peering connections, direct connects etc. 

### Costs
* Incoming traffic is free
* Comms between the same AZ is free
* AZ <-> AZ using public/EIP = cost
* AZ <-> AZ using private IP = half cost (use this wherever you can)
* Region <-> Region = cost

## Disaster Recovery

* hybrid recovery (on prem -> cloud)
* cloud native (aws region a -> region b)
* recovery **point** objective = RPO = how much data loss will occur e.g. 1 hour
* recovery **time** objective = RTO = time to recover e.g. 24h
* some strategies (sorted by highest RPO first)
  * **backup and restore** - cheap, easy but high RTO RPO
  * **pilot light** - mini app runs in the cloud with data already synced good for critical systems - smaller RTO and RPO than backup and restore
  * **warm standby** - full system running but minimum size and then switched over when needed - more expensive
  * **multi site / hot site** - full prod running in AWS + on prem - low RTO but very expensive
  * **multi region** (AWS) - AWS only but multi region for failovers

#### General Tips

**Backup**
* ebs snapshopts, rds backups + snapshots
* regular push to s3, glacier, lifecycle policy
* snowball or storage gateway

**HA**
* route 53
* RDS, Elasticache, EFS, S3 multi az
* VPN via direct connect

**Replication**
* cross region replicate + global DBs

**Automation**
* cloudformation
* cloudwatch alarm actions
* lambda functions

**Chaos**
* test using chaos on prod where possible. 

### Database Migration Service (DMS)
* secure way to migrate on prem db to AWS
* EC2 + DMS software that will auto replicate to AWS services
* sources: regular SQL servers, azure, s3
* target: regular SQL servers, RDS, DynamoDB, Redshift etc

* if SQL engines do not match use AWS Schema Conversion Tool (SCT) (runs on top of DMS)
* SCT is not needed if the agent is the same eg on prem PSQL -> RDS PSQL

### On premise strategy

* Download Linux2 AMI as iso to use with KVM etc
* Migrate VM via import/export e.g. export apps to EC2
* AWS app discovery - gather info of your on prem server and plan migrations
* AWS database migration service (DMS) - replicate on to AWS or on-prem
* AWS server migration service (SMS) - incremental replication of on prem server to AWS

### DataSync

* move data from on prem to AWS
* sync to S3, EFS, FSx
* DataSync agent required on NAS / SMB
* can also do EFS to EFS

---
#### A collapsible section with markdown
<details>
  <summary>Click to expand!</summary>
  
  ## Heading
  1. A numbered
  2. list
     * With some
     * Sub bullets
</details> 
