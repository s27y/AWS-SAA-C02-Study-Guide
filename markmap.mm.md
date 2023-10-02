---
markmap:
  colorFreezeLevel: 3
---

# Identity Access Management (IAM)

## IAM Simplified
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


# Simple Storage Service (S3)

## S3 Simplified
- Secure, durable, scalable object storage
- Object storage: data, metadata, unique identifier
- Suitable for hosting files, not databases
- Key differences from block storage

## S3 Key Details
- Objects: key, value, version ID, metadata
- Data consistency model
  - Immediate read access for new objects
  - Immediate read access for PUTS and DELETES  of existing objects
- Durability guarantee: 99.999999999% (11 9s)
- Main features: tiered storage, lifecycle, versioning, encryption, MFA delete, access control
- Charges by: storage size, requests, tiers, data transfer, transfer acceleration, replication
- Bucket policies secure data at bucket level
- Access control lists secure data at the more granular object level
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

## S3 Encryption
- Encryption in transit (SSL/TLS)
- Encryption at rest: server-side or client-side
- Server-side encryption options
  - S3 Managed Keys
  - AWS KMS
  - Customer Provided Keys

## S3 Versioning
- Stores all versions of an object
- Useful for backup, rollbacks
- Integrates with lifecycle rules
- MFA delete for added security

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

## S3 Pre-signed URLs
- A pre-signed URL grant time-limited permission to download or view private S3 object
- When create a pre-signed URL
  - Security credentials
  - bucket
  - object key
  - HTTP method
  - expiration date and time

## S3 Select
- Pull out only the data you need from an object
- Works with Glacier too

# CloudFront

## CloudFront Simplified
- AWS CDN service
- Cache content at edge location (catche endpoints)
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
- sutting-down
- terminated

## EC2 Security
- You are responsisble for management of the guest OS and anything within the OS and the config of the AWS
-Termination protection is disabled by default
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
- placement group name within your AWS must be unique
- existing EC2 can be moved into a placement group via CLI or AWS SDK


# Elastic Block Store (EBS)

## EBS simplifed
- durable, block-level storage to be attached to a single EC2

## EBS Key Details
- life cycle differs from EC2 instance
- is automatically replicated within its AZ
- 5 types
  1. General Purpose SSD (GP2)
  2. Provisioned IOPS SSD (IO1) - build for speed
  3. Throughput Optimized HDD (ST1) - built for larger data loads
  4. Code Hard Disk Drive (SC1) - lowest cost storage, built for less frequently accessed workloads
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
- point in time copies of volumes
- constrained to the region it was created
- only capture the state of the change from when the last snapshot was taken
- the first snapshot takes some time to create
- happens asynchronously, volume can be used as normal
- best pratices to stop the running instance for a clean snapshot for a future root device
- snapshot can be used to move ec2 instance and volume to another az/region
- can't delete a snapshot of an ebs vloume that is used as the root device of a registered AMI

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
- Enhanced Networking ENI for high network throughput
- Enhanced Networking ENI uses signle root I/O virtualization
- SR-IOV means higher I/O and lower throughput and higher bandwidth, high packet per second performance, consistently lower inter-instance latencies
- no extra charge for enhanced networking ENI, but not avaibleable on all ec2
- ENI can be attached when EC2 is running, stopped or being lauched
- ENI can be moved to different EC2
- Use Elastic Fabric Adaptor (EFA) for machine learning and high performance computing
- EFA support OS-bypass

# Security Groups
## Security Groups Simplified
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


