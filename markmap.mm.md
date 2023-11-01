---
markmap:
  colorFreezeLevel: 3
---

# Identity Access Management (IAM)

## IAM Simplified
- Uni
- Centralized control hub within AWS
- Integrates with all other AWS Services
- Share access at various permission levels
- Identity federation for temporary or limited access
- MFA support
- Custom password rotation policy
- PCI DSS compliant

## IAM Entities
- Users (individual end users)
- Groups (collections with shared permissions)
- Roles (permissions for software services)
- Policies (rule sets for access)

## IAM Key Details
- Global AWS service
- Root account = complete admin access
- New users have no initial permissions
- Access key ID and secret access key for programmatic access
- IAM roles can be assumed by external services
  - For example, IAM role can be assumed by one of the Active Directories for SSO
- IAM roles can be assigned to services before/after creation
- Cannot nest IAM groups
- Use tags for resource access control

## Priority Levels in IAM
- Explicit Deny
- Explicit Allow
- Default Deny (Implicit Deny)

## IAM Security Tools
- IAM Access Advisor (user level)
- IAM Credentials Report (account level)

## Secure AWS Root Account
- Enable MFA on root account
- Create admin group for admin users, assign appropriate permissions to this group
- Create user account for admin
- Add users to amdin group

# active directory
- lift and shift - managed microsfot ad
- ad is staying on-premises - use ad connector

# Simple Storage Service (S3)

## S3 Simplified
- Secure, durable, scalable object storage
- Object storage: data, metadata, unique identifier
- Suitable for hosting files, not databases
- Key differences from block storage
- upto 5TB

## S3 Key Details
- Objects: key, value, version ID, metadata
- Data consistency model
  - Immediate read access for new objects
  - Immediate read access for PUTS and DELETES  of existing objects
- Durability guarantee: 99.999999999% (11 9s)
- Main features: tiered storage, lifecycle, versioning, encryption, MFA delete, access control
- Charges by: storage size, requests, tiers, data transfer, transfer acceleration, replication
- Bucket policies secure data at bucket level
- Object Access control lists(ACLs) secure data at the more granular object level
- All newly created buckets are private (default)
- S3 access logs can be shipped into another bucket in either current or separate account
- To share S3 bucket across AWS accounts
  - Share entire buckets, use IAM & Bucket Policies, programmatic access only
  - Share objects, use ACLs & Bucket Polices, programmatic access only
  - Use cross-account IAM roles, for acess via console & the terminal
- Great for static website hosting
  - index.html and error.html

## S3 Storage Classes
- S3 Standard: high availability, durability
- S3 Infrequent Access (IA): lower cost, retrieval charges
- S3 One Zone IA: lower cost, no high availability
- S3 Intelligent Tiering: ML/AI-based tier selection
- S3 Glacier: low-cost data archiving, retrieval options
  - Retrieval methods
    - Expedited: 1 - 5 minutes
    - Standard: 3 - 5 hours
    - Bulk: 5 - 12 hours
- S3 Deep Glacier: lowest-cost storage
- S3 Glacier Instant Retrieval

## S3 Encryption
- Encryption in transit (SSL/TLS)
- Encryption at rest: server-side or client-side
- Server-side encryption options
  - S3 Managed Keys
  - AWS KMS
  - Customer Provided Keys
- Can enforcing encryption with a bucket policy

## S3 Versioning
- Stores all versions of an object
- Useful for backup, rollbacks
- cannot be disabled once enabled
- Integrates with lifecycle rules
- MFA delete for added security

## S3 Object Lock and Glacier Vault Lock
- S3 Object Lock to store objects using a write once, read many (WORM) model
- Governace mode
  - user can't overrite or delete an obj or alart it's lock unless they have special permissions
- Compliance mode
  - stop anyone to overrite or delete an object
- S3 Galcier Vault Lock
  - apply to Glacier

## S3 Lifecycle Management
- Automates data movement between storage tiers
- Applies to current and previous versions

## S3 Cross Region Replication
- Works with versioning enabled
- Replicates new uploads and updates
- Deletes not replicated

## S3 Transfer Acceleration
- Uses CloudFront network for faster data transfer
- Improved performance and reduced costs

## S3 Event Notifications
- Receive notifications on bucket events
- Destinations: Amazon SNS, Amazon SQS, AWS Lambda

## S3 and ElasticSearch
- ElasticSearch integration with S3 and Lambda
- Search through log data stored in S3

## Maximizing S3 Read/Write Performance
- Use sequential data-based naming for your prefixes to imporve performance
- Use CloudFront for performance optimazation 

## S3 Server Access Logging
- Provides detailed records made to a bucket
- Disabled by default

## S3 Multipart Upload
- Upload large objects in parts parallelly to boost efficiency
- Recoomended for file over 100MB, Only way to upload files over 5GB
- Retransimit failed part without affecting other parts
- Parallelize downloads using byte-range fetches

## S3 Select
- Pull out only the data you need from an object
- Works with Glacier too
- S3 byte-range fetches

## S3 Pre-signed URLs
- A pre-signed URL grant time-limited permission to download or view private S3 object
- When create a pre-signed URL
  - Security credentials
  - bucket
  - object key
  - HTTP method
  - expiration date and time

## S3 Replication
- replicate objects from one to anther
- existing objects are not replicated automatically
- Delete markers are not replicated by default


# CloudFront

## CloudFront Simplified
- AWS CDN service
- Cache content at edge location (catch endpoints)
- Cache origin,  can be an EC2 instance, an S3 bucket, an Elastic Load Balancer or a Route 53 config

## CloudFront Key Details
- Cache has TTL
- works with dynamic, static, streaming and interactive content
- Requests are routed and cached in the nearest edge location
- can distribute web content and RTMP(streaming ,adobe)
- Edge location can take read and write request
- manual invalidate or clear beyond TTL incur cost
- Invalidate can be done for certain object or entire directory
- Two origin in size an origin group can be setup for failover
- SSL support on edge location
- Need to log usage data
  - Enable CloudFront access logs
  - Capture requests that are sent to the cloudFront API
- Origin Access Identity (OAI) for sharing private content
- add HTTPS to a static website hosted in S3

## CloudFront Signed URLs and Signed Cookies
- Allow you to control who can access your content
- Use signed URLs for 
  - RTMP distribution
  - restrict access to individual files
  - client doesn't support cookies
- Use signed cookies for
  - Access to multiple restricted files
  - don't want to change current URLs

# Snowball

## Snowball Simplified
- A giant physical disk for migrating high quantities of data into AWS

## Snowball Key Details
- Secure and quick data transfer for TBs to PBs of data into AWS
- for low speed network
- remote location


## Snowball Edge and Snowmobile
- Snowball Edge comes with both compute and storage
- Snowmobile is for an exabyte-scale data transfer

# Storage Gate

## Storage Gateway Simplified
- It connects on-premise enviornments with cloud-based storage
- File Gateway, Volume Gateway, Tape Gateway
- S3 is the backend in AWS

## Storage Gateway Key Details
- can either be physical device or VM, act as a bridge
- can set on VMVare's ESXi or Microsoft's Hyper-V hypervisor
- File Gateway
  - NFS or SMB, file system mount on S3
- Volume Gateway
  - iSCSI, store copies of hard/virtual disk in S3
- Tape Gateway
  - Virtual Tap Library
- File metadata is stored as metadata
- Data written to Volume Gateway can be async backed up into EBS as point-in-time snapshots

## Stored Volumes vs. Cached Volumes
- Stored Volumes stores data locally on-prem and backs up to AWS
- Cached Volumes, AWS is used as primary data source and local hardware is used as a chaching layer


# Elastic Compute Cloud (EC2)

## EC2 Simplified
- resizeable server that can scale up and down quickly
- Charged on CPU, memory, storage, and networking. When stopped, only charged for EBS storage

## EC2 Key Details
- Amazon Machine Image (AMI) can be used to launch multiple instances
- Dedicated tenacy means you have exclusive access to physical hardware
- EC3 VM Import can import existing VMs into AWS as long as those hosts use VMware ESX VMware Workstation, Microsoft Hyper-V, or Citrix Xen
- User data is for running common automated configuration tasks or scripts
- By defaults, public IP address of EC2 isntance is released when the instance is stopped
- use Elastic IP address when static IP address is needed
- golden image is an AMI that you have fully customized
- Instance status checks check the helath of the running EC2 server
- System status check monitor the health of the underlying hyperviosr
- Stop and start when there is a system status issue.

## EC2 Instance Pricing
- On-Demand instances
  - fixed rate by the hour or second
  - no long-term commitment
- Reserved instances
  - long-term commitment (1 or 3 years contract)
  - up to 75% discount compared to On-Demand
- Spot instances
  - bid for spare computing capacity
  - up to 90% discount compared to On-Demand
  - can be terminated at any time
- Dedicated
  - a physical EC2 server dedicated for your use
  - mainly for server bound licenses or complicance requirements
    - Windows Server, Microsoft SQL Server, SUSE Linux Enterprise Server

## Standard Reserved Instances vs. Convertible Reserved Instances vs. Scheduled Reserved
- Standard Reserved Instances
  - 75% discount
  - cannot be moved between regions
- Convertible Reserved Instances
  - 54% discount
  - can be moved between regions
  - can be changed to different instance types
- Scheduled Reserved Instances
  - launch within time window you reserve


## EC2 Instance Lifecycle
- Pending
  - not billed
- running
  - billed
- stopping
  - not billed if preparing to stop
  - billed if preparing to hibernate
- stopped
  - not billed
- shutting-down
- terminated

## EC2 Security
- You are responsisble for management of the guest OS and anything within the OS and the config of the AWS
- Termination protection is disabled by default
- public-key (key pair) is used to encrypt the passed password
- root volume can be encrypted at creation time
- additional volumes can be encrypted using EBS encryption
- EBS root volume will be deleted with instance however additional volumes will not be deleted.

## EC2 Placement Groups
- it balances the tradeoff between risk tolerance and network performance
- Clustered Placement Group
  - single AZ, for apps need the lowest latency and highest network throughput
  - only certain instances type can be launched
- Spread Placement Group
  - seperate racks, separate power and network
  - multiple AZ, for apps that have a small number of critical instances that should be kept separate from each other
  - can span multiple AZ
- Partitioned Placement Group
  - multiple EC2 within a single partition, failures only affect a signle partition
  - HBase, HDFS, Cassandra
- placement group name within your AWS must be unique
- existing EC2 can be moved into a placement group via CLI or AWS SDK
- only X optimiazed instance types can be launched in a placement group
- can move an existing instance into a placement group - when they are stopped

## vCenter on AWS using VMware

## EC2 Hibernation
- preserves the in-memory RAM on persistent storage
- fater to boot up
- instace Ram must be less than 150GB
- cannot be hibernated for more than 60 days

## AWS Outposts
- extend AWS to your data center
- AWS outpost rack and servers

# Elastic Block Store (EBS)

## EBS simplifed
- durable, block-level storage to be attached to a single EC2

## EBS Key Details
- life cycle differs from EC2 instance
- is automatically replicated within its AZ
- 5 types
  1. General Purpose SSD
    - gp2
    - gp3 - faster
  2. Provisioned IOPS SSD - build for speed
  3. Throughput Optimized HDD (ST1) - built for larger data loads
    - cannot be a boot volume
  4. Code Hard Disk Drive (SC1) - lowest cost storage, built for less frequently accessed workloads
    - cannot be a boot volume
  5. Magenetic
- 5 9s durability
- EBS need to be in the same AZ as the EC2 instance
- can be attahced to a single EC2
- snapshots are point-in-time copies of EBS
- The size and type of EBS volumes can be changed on the fly,

## SSD vs. HDD
- SSD
  - built for transactional workloads
  - frequent read/write
  - IOPS heavy
- HDD
  - built for large streaming workloads
  - throughout heavy
  - MB/s heavy


## EBS Snapshots
- stored in S3
- point in time copies of volumes
- constrained to the region it was created
- only capture the state of the change from when the last snapshot was taken
- the first snapshot takes some time to create
- happens asynchronously, volume can be used as normal
- best pratices to stop the running instance for a clean snapshot for a future root device
- snapshot can be used to move ec2 instance and volume to another az/region
- can't delete a snapshot of an EBS vloume that is used as the root device of a registered AMI

## EBS Root Device Storage
- EBS-backed or Instance store-backed
- EBS-backed
  - root device is an EBS volume
  - default
  - root device is persistent
  - can be stopped and started
  - can be changed on the fly
- Instance store-backed
  - very high IOPS
  - root device is an instance store volume (from an S3 stored template)
  - root device is ephemeral
  - cannot be stopped and started
  - cannot be changed on the fly
  - secondary volumes backed by instance store must be installed during original provisioning
- When to use one over the other
  - EBS for DB data, critial logs and application configs
  - Instance store for temporary data, buffers, caches, scratch data, and other temporary content

## EBS Encryption
- AWS KMS CMK to create encrypted volumes and snapshots
- AES-256 encryption
- can only share unencrypted snapshots
- volume created from encrypted snapshot are encrypted automatically
- root device of EC2 can be encrypted at provisioning time

# Elastic Network Interface (ENI)

## ENI simplified
- virtual network card

## ENI Key Details
- low-budget, high-availability
- Enhanced Networking ENI 
  - for high network throughput
  - uses signle root I/O virtualization
  - between 10 Gbps AND 100 Gbps
- SR-IOV means higher I/O and lower throughput and higher bandwidth, high packet per second performance, consistently lower inter-instance latencies
- no extra charge for enhanced networking ENI, but not avaibleable on all ec2
- ENI can be attached when EC2 is running, stopped or being lauched
- ENI can be moved to different EC2
- Use Elastic Fabric Adaptor (EFA) for machine learning and high performance computing
- EFA support OS-bypass

# Security Groups
## Security Groups Simplified
- stateful
- controle access with EC2
- Act as virtual firewall
- on instance level

## Security Groups Key Details
- Controle in/out bound tracffic for EC2 instances, typically it will have port in it.
- NACLs for subnets, and typicaly it will have IP in it
- stateful
- rules are based on ALLOWs
- everything is blocked by default
- can't be shared between VPCs
- regional and can span AZs, but can't be cross-regional


# Web Application Firewall (WAF)

## WAF Simplified
- allow or block traffic that are bound for cloudfront, ALB, API Gateway, ec2, and other L7 entry points
- use security rules to block common attack patterns, for example SQL injection or cross-site scripting and rules that filter out specific traffic patterns that you define


## WAF Key Details
- L7 firewall
- monitor granular web-based conditions like URL query string parmeters
- allow all requests except the ones you specify
- block all requests except the ones you specify
- count the requests that match the properties that you specify

## WAF Protection Capabilities
- request cahacteristics that can be used to limit access
- ip address
- country
- header
- strings in request matches a regex parttern
- length of the request
- any presence of sql code 
- any presence of script code
- WAF added the advantage of protecting from its outermost border


# CloudWatch

## CloudWatch Simplified
- monitor AWS resources and applications

## CloudWatch Key Details
- collects monitoring and operational data in the form of logs, metrics and events
- ec2, only monitor host level metrics and status from the underlying hypervisor
- ec2, default to 5 minutes, but can have 1 minute with detailed monitoring
- cloudwatch agent can be installed on ec2 to collect custom metrics
- cloudwatch is all about performance
- cloudtrail is all about auditing

## cloudwathc logs
## cloudwatch events
## cloudwatch alarms
## cloudwatch metrics
## cloudwatch dashboards

# CloudTrail

## CloudTrail Simplified
- enables governance, compliance, operational auditng and risk auditing of your aws account
- records all api calls made within your aws account
- regional, but can be aggregated across regions and accounts

## CloudTrail Key Details
- logs api calls or activites
- stores last 90d of events in event history, default no additional charge
- two types of events, management events(default on) and data events(default off)
- log files are encrypted using aws s3 server-side encryption. it can be encrypted using aws kms

# Elastic File System (EFS)

## EFS Simplified
- EFS  = AWS elastic NFS
- automatically and instantly scales

## EFS Key Details
- EFS can be attached to multiple ec2 instances
- uses NFSv4 protocol, need open EC2 security group
- pay per use, no pre-provisioning required
- can scale up to petabytes to support thousands of concurrent NFS
- read after write consistency
- data is stored across multiple AZs within a region
- read-after-write consistency

# Amazon FSx for Windows

## Amazon FSx for Windows Simplified
- a fully managed native Microsoft File System

## Amazon FSx for Windows Key Details
- solely for Microsoft-based application
- SMB-based file storage
- on-premise server can connect to FSx
- Microsoft AD can be used to authenticate
- encrypt data at rest and in-transit
- single AZ or multi-AZ
- SSD or HDD
- daily automated backups and on demand backup
- remove duplicated content and compresses common content

# Amazon FSx for Lustre

## Amazon FSx for lustre Simplified
- open source Lustre file system for high performance computing
- up to hundreds of gigabytes per second of throughput, millions of IOPS, sub-millisecond latencies

## Amazon FSx for Lustre Key Details
- Linux system
- typically run on compute clusters
- can store and retreve data directly on S3


# Relational Database Service (RDS)

## RDS Simplified
- managed service

## RDS Key Details
- Six different flavors
  - SQL Server
  - Oracle
  - MySQL Server
  - PostgreSQL
  - MariaDB
  - Aurora
- RDS is a DB engine which DBs sit on top of
- Read replication
- Multi-AZ for high availability
- runs on VM that you do not have access to.
- AWS does security and maintence
- SQS queue can be used to store pending db writes

## RDS Multi-AZ
- used for disaster recovery
- primary DB and synchronouly replications in diferent AZ
- connect to RDS uses DNS address. parmary DB fails, multi-az automaticlly update the DNS to point it to secondary
- support all DB flavor except aurora, as aurora is complete fault-tolerant
- high availability across az and not regions
- force failover by rebooting primary instance
- backups are taken from the standby

## RDS Read Replicas
- for scaling read performance, not for disaster recovery
- if master failed, no automatic failover.
- auto backups must be enabled to use read replicas
- up to 5 read replications
- supported for all DB on top of RDS
- use DNS address for connection. write is received by master also passed onto secondary
- promote read replicas to be their own production db
- read replica has its own DNS endpoint
- works with Multi-AZ, or have it in an entirely separate region

## RDS Backups
- Automate backups
  - any point in time within 35 days
  - freely up to the size of your actual db
  - removed when DB is removed
- DB snapshots
  - done manually
  - will retain enven the original RDS is terminated
- Restore a DB via automated backups or DB snapshots results an entirely new RDS instance

## RDS Security
- IAM DB authentication
  - works with MySQL and PostgreSQL
  - authentication token
    - lifetime of 15 minutes
  - traffic to/fram DB is SSL encrypted
  - centrally manage access in IAM
- encryption at rest supprot all DB, AWS KMS
- encryption can be enable only when you create it

## RDS Enhansced Monitoring
- metrics in cloudwatch log for 30 days
- agent based

# Aurora

## Aurora Simplified
- MySQL/PostgreSQL compatible RDBMS

## Aurora Key Details
- automatic failover
- typically created as a cluster of DB instances
- default 2 copies in 3 availability zone, loss upto 2 without impact wirte, 3 without impact read
- self-healing, data blacks and disk are constiuously scanned for error
- Aurora relication can be both a standy and a target for read traffic
- up to 15 copies
- automated failover is only possible with Aurora read replication
- backup doesn't impact performance
- to migrating rds db into aurora db
  - create a read replica of a rds mariadb/mysql db as aurora db
  - promote aurora db into prod instance
  - delete old db
- from 10GB to 128TB, Computing up to 32vCPUs and 244GB memeory

## Aurora Serverless
- - on-demand or auto scaling database
- for infrequent, intermittent, and unpredictable workloads
- pay per invocation

## Aurora Cluster Endpoints
- map each connection to the appropriate instance or group of instances based on use case

## Aurora Reader Endpoints
- up to 15 read replicas

# DynamoDB
## DynamoDB Simplifed
- stored on SSD
- spread across 3 geo distinct dc
- eventually consistent reads(default)
- strongly consistent read
- full backup at any time
- no impact on performance or availability
- point-in-time recovery
  - in last 35 days, latest 5 minutes in the past

## DynamoDB Accelerator (DAX)
- managed, HA, in-memory cache
- up to 10-node cluster
- one to many or many to one for DAX cluster for DDB tables

## DynamoDB Streams
- an ordered flow oof information about changes to iteams in DDB table
- capture data modification events
- it can trigger lambda function

## DynamoDB Global Tables
- multi-region, multi-master
- replication latency < 1 second

# Amazon DocumentDB
- MongoDB

# AWS Keyspaces
- Cassandra

# AWS Neptune
- graph database

# AWS Quantum Ledger Database (QLDB)
- immutable databases

# AWS Timestream
- to store a large amount of time-series data for analysis


# Redshift

## Redshift Simplified
- manged PT-scale data warehouse

## Redshift Key Details
- single-AZ
- consists of leader node and compute nodes(up to 128)
- for OLAP
- add remove nodes on the fly
- replication to different region
- HA cluster requires 3 copies of your data, one in redshift, other in S3
- billed for 
  - computing nodes hours
  - backups
  - data transfer within VPC
- locked by default using security group

## Redshift Spectrum
- run SQL queries against exabytes of data in S3
- no loading or ETL required
- cluster and data must in same region
- read only on s3 data

## Redshift Enhanced VPC Routing
-  force all COPY and UNLOAD traffic between cluster and data in VPC

# EMR
- made up EC2
- Apache Hadoop and Apache Spark

# ElastiCache
## ElastiCache Simplified
- in-memory data store

## Elasticache Key Details
- fully managed Redis and Memchched
- Memcached for simple caching purposes with multi-threaded performance
- it scales

# Route53

## Route53 Simplified
- DNS service
- domain registration
- DNS routing
- health checking

## Route53 Key Details
- SOA (Start of Authority) record
  - domain name
  - email of admin
  - domain serial number
  - TTL
- NS (Name Server) record
  - used by the Top Level Domain hosts(.org, .com, .uk)
  - domain name
  - name server
  - TTL
- Browser -> TLD -> SOA -> DNS
- A record
  - hostname to IPv4
- AAAA record
  - URL -> IPv6
- CName
  - hostname -> hostname
  - can't be used for naked domain names
- Alias
 - URL -> AWS resource
- PTP
  - IPv4 -> hostname

## Health Checks
- can be associated with DNS records
- if record failed health check, it will be removed from route53 until it passes the health check


## Route53 Routing Policies
- Simple
- Weidghted
  - split traffic based on different weights assigned
- Latency-based
- Failover
  - active-passive
- Geolocation Routing
- Geo-proximity
  - similar to Geolocation routing, but you can choose to send more or less traffic
  - must enable route53 traffic flow
- Multivalue
  - similar to simple routing but with a health check on each record set


# ELB
## ELB Simplified

## ELB Key Details
- regional service
- it is resolved using DNS
- inService or OutOfService status, health check
- 504 error means application issue (not responding within the idel timeout period)
- Application LBs
  - L7
  - HTTP(S)
  - path-based routing
  - host-based routing
  - TLS termination
  - support sticky sessions on target group level
- Network LBs
  - L4
  - TCP tracffic
  - high performance, low latency
  - support static ip
- Classic LBs
  - L4 and L7
  - HTTP, HTTPS, TCP
  - EC2-Classic

## ELB Advanced Features
- X-Forwarded-For header for backend server to know the origin of the traffic
- Sticky sessions 
- Path Patterns

## ELB Cross Zone Load balancing
- distribute traffic evenlly across different AZs

## ELB Security
- support SSL/TLS & HTTPS termination
- Perfect Forward Secrecy
  - key changes over time
- SNI support ALB or CloudFront

## Sticky Session
- enable your users to sick to the same EC2 instance

## Connection Draining
- Deregistration Delay
  - enable it - keep existing conn. open if the EC2 instance becomes unhealthy
  - disable it - immediately close connection if the EC2 instance becomes unhealthy

# Auto scaling
## Key Details
- Components
  - Groups
    - groups of EC2 or DB
  - Configuration Templates
  - Scaling Options
- auto scale
- can maintain current instance levels
- support manual intervention
- scheduled scaling
- predictive scaling (ML)
- can suspend and then resume scaling process for debugging
- lunch configuration can't be changed after it's creation

## Auto Scaling Default Termination Policy
- default to terminate a stopped instance
  - instances in multiple AZ, terminate from AZ with most instances
  - instances in same AZ, terminate the instance with the oldest launch configuration
  - terminate instance closest to the next billing hour

## Auto scaling cooldown period
- ensure it doesn't launch or terminate additional instances before the previous scaling activity takes effect
- default 300 seconds

# Virtual Private Cloud (VPC)
## VPC Simplicfied 
- create logically isolated section of AWS

## VPC Key Details
- complete control of your own network, ip, subnet, route table, network gateways, and security settings
- default VPC on aws allow internet access
- create integer gateway for internet access
- IGW need be assigned to a VPC
- a custom VPC comes with
  - route table
  - NACL
  - secuirty group
- default ip range /16
- all instances within VPC has a private IP
- launch an instance in subnet with public access via internet gateway. public and private ip is created


## VPC Subnets
- aws reserve 5 ip address within subnet, first 4 and last 1

## Network Access Control Lists
- stateless
- start from the lowest number to high number
- each rule can either allow or deny traffic
- default NACL allow all inbound and outbound traffic
- new NACL default rules deny all in and out
- use it to block IP address

## NAT instances vs. NAT Gateways
- NAT Gateways
   - no security group need
   - automatically get public ip assigned
- internet gatway is for instance in VPC that already have a public ip
- one IgW for each VPC
- one NAT for each AZ
- NAT is for instance in VPC that don't have a public ip
- NAT instances
  - individual EC2 instance
  - HA is not built-in
- NAT gateway
  - managed service
- disable source/destination check when using NAT instance


## Bastion Hosts
- jump box
- reduce attack
- allow remote access to private subnet
- a small EC2 instance 

## Route Tables
- best practice is to ensure default route table is private
- can be used to configure access to AWS endpoint

## Internet Gateway
- each ec2 instance doesn't know it's public ip, only IGW knows it's public ip
- one IGW per VPC

## Virtual Private Networks (VPNs)
- connect on-prem to AWS

## AWS DirectConnect
- connect on-prem and AWS through a private tunnel

## VPC Endpoints
- connect VPC to supported AWS service, traffic stay within AWS
- Gateway Endpoint
   - point traffic to a route table entry
   - currently support S3  and DynamoDB
   - free
- Interface Endpoints
  - it uses AWS PrivateLink and private IP
  - ues ENI in VPC

## AWS PrivateLink
- private connectivity between different VPCs, AWS services
- connects your AWS services with other AWS service through a non-public tunnel


## VPC Peering
- connect one VPC wither another via a direct network route using private IPs
- cannot do transitive peering
- can't do peering
  - overlapping cidr  block
  - transitive peering
  - edge to edge routing
- can peer across regions or accounts

## Transit Gateway
- to use route table to limit how VPCs talk to one another
- iwht with Direct Connect as well as VPN connection
- support IP multicast

## VPN hub
- office in one city to talk to office in another city via VPN

## VPC flow log
- capture ip info for all traffic flowing in and out of VPC
- stored in s3 bucket, view in cloudwatch
- traffic flow
  - in and out of vpc
  - in and out of subnet
  - in and out of ec2 network interface
- can't change existing flow log config
- not monitored
  - query for instance metadata
  - dhcp
  - query to aws dns

## AWS Global Accesserator
- reduce hops to your aws service

# Simple Queuing Service (SQS)
## SQS Simplified
- a message queue that can store messages before another service process them

## SQS Key Details
- standard
  - may out of order
  - delivered at least once (means it can duplicate message)
- FIFO
  - guarantee order
  - exactly-once
  - limited to 300 transactions per second
- message in queue can be kept from 1 minutes to 14 days, default to 4 days
- visibility timeout
  - when a message is send to a reader, the message is temporarily marked invisble, if the message is not fully processed within the time limit, the message becomes vidible again
  - max is 12 hour

## SQS Polling
- Long-polling
  - only return from the queue when there is a message
  - or it will wait until timeout
- Short-polling
  - retrun immediately either there is a message or not
- receivedMessageWaitTimeSeconds is the attributes to determines Short or Long
- polling incur a charge

# Simple Workflow Service (SWF)
## SWF Simplified
- coordinate work across distributed application

## SWF Key Details
- a way of coordinating tasks between app and people
- Actor
  - workers that trigger the begining of a workflow
- Decider
  - workers that control the flow of the workflow once it's been started
- Activity Worker
  - workers that actually carry out the task
- workflow execution can last up to one year

# Simple Notification Service (SNS)
## SNS Simplified
- pushed-based message service.

## SNS Key Details
- mainly used to send alarms or alerts
- high-throughput, push-based, many-to-many messaging
- SNS topcs
  - fan out message to large number of subscrber
  - via SQS, lambda, http/s webhooks, mobile push, sms and email
- topcis used to group multiple recipient

# Kinesis
## Kinesis Simplifed
- collect, process and analyze real-time, streaming data
- video, audio, application logs, website clickstreams, IoT telemetry

## Kinesis Key Details
- Kinesis Streams
  - retain from one day up to 7 days
  - data is contained within shards
- Kinesis Firehose
  - load stream data into data stores and analytics tools
  - capture, transform, and load streaming data to different source
- Kinesis Analytics
  - work with two above, can analyze data on the fly
- partition key
  - organize data by shard
  - maintain order within shard

# Lambda
## Lambda Simplified
- run code without provisioning or managing servers

## Lambda Key Details


# API Gateway
## Key Details
- create, publish, maintain, monitor, and secure APIs at any scale
- pay for api calls received and amount of data transfered out
- provide throttling
  - request over limit receive 429
- cache is supported
- support AWS certificate manager

## Cross Origin Resource sharing
- enforced on client side

# CloudFormation
## Simplified
- tool for provisioning cloud-based env

# Key Details
- create, update, delete infra
- template is json or yaml
- a full CF setup is called a stack
- Resources field is the only mandatory field

# Elastic Beanstalk Simplifed
- simple solution

# AWS Organization
## Simplified
- accoutn management service
## Key Details
- root account to manage billing, separate accounts to deploy resource
- centrally govern envrionment
- Organizational Units (OU) to group accounts
- Attach policies to OU
- Service Control Policies (SCP) to restrict access to certain services
- centralized logs


# Amazon Cognito
- Web Identity Federation
- authenticate with identity provider, get token, exchange token for temporary AWS credentials
- Cognito User Pools
  - user directory
  - sign up and sign in
  - can be used with API Gateway
- Cognito Identity Pools
  - provide AWS credentials to users
  - can be used with Cognito User Pools
  - can be used with Facebook, Google, Amazon, Twitter, Digits, and any OpenID Connect

# AWS Resrouce Access Manager
- a service enables you to share AWS resrouces with any AWS account
- no need to create duplicate resources in multiple accounts

# Athena
- Serverless SQL
- interactive query service for data stored in S3

# Glue
- Serverless ETL service
- it can help create that schema for your data when paired with Athena

# AWS Macie
- ML-powered data security and privacy service
- discover, classify, and protect sensitive data (PII) in S3
- Macie alerts
- HIPAA, GDPR compliance
- automate remediation action using other aws services

# AWS KMS
- shared tenancy of underlying hardware
- managed service that makes it easy for you to create and control the encryption keys used to encrypt your data
- to control permissions
  - use key policy
  - use iam policies in combination with key policy
  - use grants in combination with the key policy

# CloudHSM
- dedicated HSM
- no automatic key roation


# AWS Secrets Manager
- store application secrets
- apps can use secrets manager api
- easy to roating creds

# parameter store


# AWS STS
- create and provide trusted users with temporary security credentials

# OpsWOrks
- AWS managed configuration management service for  Chef and Puppet

# Elastic Transcoder

# AWS Directory Service
- Amazon Cloud Directory, Microsft AD, AD Connector, Simple AD

# IoT Core
- managed service that lets connected devices easily and securely interact with cloud applications and other devices

# AWS Farget
- serverless compute for containers
- ECS and EKS

# AWS EKS
- fully manage K8s 

# Amazon MQ
- managed messaging broker service
- Support ActiveMQ and RabbitMQ

# AWS Config
- assess, audit, and evaluate the configurations of your AWS resources

# AWS Wavelength
- increasing app speed at edge using mobile networks

# AWS Batch
- Long-running (>15minutes), batched workload
- queued workloads
- on-demand alternative to AWS lambda

# AWS Step Functions
- coordinate multiple AWS services into serverless workflows
- up to 1 year

# AWS AppFlow
- Saas data ingestion service
- ingest data from external SaaS apps into AWS
- Bi-directional

# QuickSight
- Creating a dashboard

# OpenSearch
- analyzing log files and various documents, especially within an ETL process

# Data Pipeline
- managed ETL
- integrate service with within AWS, like RDS, S3, EC2 and EMR
- Data-driven and task-dependent ETL workload

# AWS Managed Streaing for Apache Kafka (MSK)
- managed service that makes it easy for you to build and run applications that use Apache Kafka to process streaming data
- you manage data plane operation

# AWS X-Ray
- used to gain apps insightes using requests and responses of services and functions
- Traces downstream response time

# AWS AppSync
- Manage GraphQL

# Shield
- protects against L3 and L4
- DDoS
- free
- advanced cost 300usd but with dedicated 24/7 reponse team

# AWS Firewall Manager
- multiple AWS accounts and resouces that need to be secured cetrally

# GuardDuty
- use ai to learn normal behavior
- alert you abnormal or malicious behavier
- monitors logs (CloudTrail, VPC flow, DNS)

# Inspector
- perform automate vulnerability scans on both EC2 instances (host assessments) and VPCs (network assessments)

# Detective
- operates across multiple AWS service
- analyzes the root cause of an event

# Audit Manager
- continuous and automating auditing reports

# AWS Artifact
- audit and the need for compliance reports

# Security Hub
- a single place to view all your security alerts across multiple services and accounts

# Certificate Manager
- support ELB, CLOUDFRONT API GATEWAY
- free, auto renew and rotate

# Global Accelerator
- 2 static IP address
- avoid IP caching 

# AWS Conifg
- standarization - a rule need be setup for an account use config to check ofr compliace
- automate reponse to remediate problems using automation documents
- one-stop shop to what's changed

# Compute Optimizer
- generate recommendations on implmenting more accurate compute size

# Trusted Advisor
- auditing tool
- use eventbridge to kick off lambda

# AWS Control Tower
- multi-account env
- preventive or detective guardrails

# AWS service catalog
- allow end user to provison pre-approved products and services

# Proton
- automte provisioning of app stack either container base or sls based

# AWS Health
- provide notification of both public and account-specif events within AWS
- hardware maintenance reboots

# Mindmap

## Links

- <https://markmap.js.org/>
- [GitHub](https://github.com/gera2ld/markmap)

## Related Projects

- [coc-markmap](https://github.com/gera2ld/coc-markmap)
- [gatsby-remark-markmap](https://github.com/gera2ld/gatsby-remark-markmap)

## Features

- links
- **strong** ~~del~~ *italic* ==highlight==
- multiline
  text
- `inline code`
-
    ```js
    console.log('code block');
    ```
- Katex
  - $x = {-b \pm \sqrt{b^2-4ac} \over 2a}$
  - [More Katex Examples](#?d=gist:af76a4c245b302206b16aec503dbe07b:katex.md)
- Now we can wrap very very very very long text based on `maxWidth` option


