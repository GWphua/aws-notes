# AWS

## EC2

- One of the most popular of AWS' offering
- EC2 : Elastic Compute Cloud = IAAS
- Mainly consists in the capability of
  1. Renting virtual machines (EC2)
  2. Storing data on virtual drives (EBS)
  3. Distributing load across machines (ELB)
  4. Scaling the services using an auto-scaling group (ASG)

### EC2 sizing and configuration options

1. Operating System (OS):
   - Linux
   - Windows
   - Mac OS
2. How much compute power and cores (CPU)
3. How much random-access memory (RAM)
4. How much storage space:
   - Network-attached (EBS/EFS)
   - Hardware (EC2 Instance Store)
5. Network card
   - Speed of the card, Public IP Address
6. Firewall rules
7. Bootstrap Script
   - EC2 User Data Script

### EC2 User Data Script

- A shell script that is run when EC2 instance starts.
  1. Launching commands when our EC2 instance starts.
  2. That script is only run once at the instance first start.
  3. EC2 User Data is used to automate book tasks, such as:
     - Installing updates, software.
     - Downloading common files from the internet.

### Key Pair

- Necessary if we use the SSH utility to access the EC2 instance.
- Private key file formats
  - .pem (For Mac, Linux, Windows 10)
  - .ppk (For Windows 7,8)

### Instance Details

1. Instance summary
   - Instance ID: Unique identifier for the instance.
   - Public IPv4P address: What we are going to use to access EC2 instance.
     - Public IP may be changed when we stop, and then start an instance.
   - Private IPv4 address: How to access the instance internally in the AWS network.
2. Security
   - Information on the security group.
   - Inbound and outbound rules: Rules controlling communication inwards and outwards.

### EC2 Instance types

#### Instance Costs

#### Free Tiers

- t2.micro (Free for up to 750hours/month)

#### Paid Tiers

- t2.xlarge
- c5d.4xlarge
- r5.16xlarge
- m5.8xlarge

#### Naming convention

      `m5.2xlarge`

- Instance class: m
- Generation: 5 (AWS improves them over time)
- Size within the instance class: 2xlarge

#### General Purpose Instance Types

- Great for a diversity of workloads such as web servers or code repositories
- Balance between Compute, Memory and Networking
- Most general purpose instance types have the _T, M, A_ name

#### Compute Optimized Instance Types

- Great for Compute-intensive tasks that require high performance processors:
  - Batch processing workloads
  - Media transcoding
  - High performance web servers
  - High performance computing
  - Scientific modeling & machine learning
  - Dedicated gaming servers
- Most compute optimized instance types have the _C_ name

#### Memory Optimized Instance Types

- Fast performance for workloads that process large data sets in memory:
  - High performance, relational/non-relational databases
  - Distributed web scale cache stores
  - In-memory databases optimized for Business Intelligence
  - Applications performing real-time processing of big unstructured data
- Most memory optimized instance types have the _R, X, z_ name

#### Storage Optimized Instance Types

- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage:
  - High frequency Online Transaction Processing (_OLTP_) Systems
  - Relational & NoSQL databases
  - Cache for in-memory databases
  - Data warehousing applications
  - Distributed file systems
- Most storage optimized instance types have the _I, D, H_ name

### Security Groups

#### Introduction to Security Groups

- Security Groups are the fundamental of network security in AWS
- They control how traffic is allowed into or out of our EC2 instance
- Security groups only contain _allow_ rules
- Security groups rules can reference by IP or by security group
- Security groups can be attached to multiple instances

#### Security Groups as a firewall

- Security groups are acting as a firewall on EC2 instances.
- They regulate
  1. Access to Ports
  2. Authorized IP ranges - IPv4, IPv6
  3. Control of inbound network
  4. Control of outbound network
- All inbound traffic is blocked by default
- All outbound traffic is authorized by default
- Security groups are locked down to a region / Virtual Private Cloud combination
- Lives _outside_ the EC2 instance
  - If traffic is blocked, the EC2 instance cannot see the inbound network
- Common errors for EC2 instances:
  - Application timeout: Security group issue
  - Connection refused error: Application error / Application is not launched
- It is good to maintain one separate security group for SSH access

### Classic ports to know

- FTP (File Transfer Protocol): _21_
  - Upload files into a file share
- SFTP (Secure File Transfer Protocol): _22_
  - Upload files using SSH
- SSH (Secure Shell): _22_
  - Logs into a Linux Instance
- HTTP: _80_
  - Access unsecured websites
- HTTPS: _443_
  - Access secured websites
- RDP (Remote Desktop Protocol): _3389_
  - Log into a Windows Instance

### SSH

#### Connectivity Summary Table

EC2 Instance Connect uses the web browser to connect to EC2 Instance, and only works with Amazon Linux 2.

|              | SSH | PuTTY | EC2 Instance Connect |
| ------------ | --- | ----- | -------------------- |
| Mac          | X   |       | X                    |
| Linux        | X   |       | X                    |
| Windows <10  |     | X     | X                    |
| Windows >=10 | X   | X     | X                    |

#### SSH using Linux or Mac or Windows >= 10

- SSH using .pem Key Pair: Navigate to the directory containing the .pem file, and enter:

  `ssh -i <File Name> ec2-user@<Public IP>`

#### SSH using Windows with PuTTY

- Install PuTTY, and open up PuTTY Key Generator to generate a .ppk file with a .pem file.
  - Remember to save as a private key with RSA key generator.
- Set up PuTTY to access the EC2 instance.
  - Enter under Host Name `ec2-user@<Public IP>`, select connection type to SSH.
  - Save this setting under the EC2 Instance.
  - Specify the key by going under SSH > Auth, and link the .ppk private key file.
- After this initial setup, we can SSH directly into the EC2 Instance.

#### SSH using EC2 Instance Connect

- Go to the EC2 Instances Page, and click on instance and press on Connect.
- A new connection page will appear on the browser.
- Sometimes, we may need to add an inbound rule to allow ip addresses with IPv6 to SSH.

### EC2 Instances Purchasing Options

#### On-Demand Instances

- Short workload, predictable pricing, and paying by second
  - Has the highest cost but no upfront payment
  - No long-term commitment
  - Recommended for short-term and un-interrupted workloads, where you cannot predict how the application will behave

#### Reserved Instances (1 & 3 years)

- Reserved Instances - Long workloads
  - Recommended for stead-state usage applications
- Convertible Reserved Instances - Long workloads with flexible instances
  - Can change the EC2 instance type, instance family, OS, scope and tenancy

#### Savings Plan (1 & 3 years)

- Commitment to an amount of usage, with long workload
  - Get a discount based on long-term usage

#### Spot Instances

- Short workloads, cheap, and less reliable as you can lose those instances
  - Instances that you can lose at any point, if your max price is less than the current spot price.
  - Useful for workloads that are resilient to failure
  - Not suitable for critical jobs or databases

#### Dedicated Hosts

- Book an entire physical server, control instance placement
  - Allows your address compliance requirements and use your existing server-bound software licenses
  - Useful for software that have complicated licensing model
  - Useful for companies that have strong regulatory or compliance needs

#### Dedicated Instances

- No other customers will share your hardware
  - May share hardware with other instances in the same account
  - No control over instance placement
    - Can move hardware after Stop / Start

#### Capacity Reservations

- Reserve capacity in a specific AZ (Application Zone) for any duration
  - No time commitment, no billing discounts
  - Can be combined with Regional Reserved Instances, and Savings Plans to benefit from billing discounts
  - Charged at On-Demand rate whether you run instances or not
  - Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ

### Shared Responsibility Model for EC2

| AWS                         | User                                                   |
| --------------------------- | ------------------------------------------------------ |
| Infrastructure              | Security Groups rules                                  |
| Isolation on physical hosts | OS patches and updates                                 |
| Replacing faulty hardware   | Software and utilities installed on the EC2 instance   |
| Compliance validation       | IAM Roles assigned to EC2 & IAM user access management |
|                             | Data security on your instance                         |

## EC2 Instance Storage

### Elastic Block Store Volume

- A network drive you can attach to your instances while they run
  - Uses the network to communicate the instance, thus meaning that there might be a bit of latency
  - Can be detached from an EC2 instance, and attached to another one quickly
  - We can also leave them unattached on creation, and attach them on-demand
- Allows your instances to persist data, even after their termination
- Can only be mounted to _one instance at a time_
  - EBS Volume types _io1, io2_ are exceptions to this rule, with them providing a EBS Multi-Attach feature.
- Bound to a specific AZ (Availability Zone)
  - An EBS Volume in _us-east-1a_ cannot be attached to an EC2 instance in _us-east-1b_
  - To move a volume across, you first need to snapshot it
- Free tier provides 30GB of free EBS storage of type SSD, or Magnetic Disk, per month
  - Has a provisioned capacity, meaning that we specify how much storage we want beforehand

#### EBS Delete on Termination Attribute

- Controls the EBS behavior when an EC2 instance terminates
  - By default, the root EBS Volume has this attribute enabled
  - By default, any other attached EBS Volume has this attribute disabled
- Can be controlled in the AWS console / AWS CLI
  - Useful when we want our data in the root EBS Volume to persist

#### EBS Snapshots

- We can make a backup (snapshot) of the EBS volume any point in time
  - Not necessary to detach volume to do snapshot, but recommended.
- Can copy snapshots across AZ or Region, meaning we can transfer data across AZ.

#### EBS Snapshot Features

- EBS Snapshot Archive

  - Move a Snapshot to an _archive tier_, that is 75% cheaper.
  - Takes within _24 to 72 hours_ for restoring the archive

- Recycle Bin for EBS Snapshots
  - Setup rules to retain deleted snapshots so you can recover them after an accidental deletion
  - Retention period can be specified
    - From 1 day to 1 year

### Amazon Machine Image (AMI) Overview

- AMI are a customization of an EC2 instance
  - You can add your own software, configuration, operating system, etc.
  - Faster boot/configuration time because all your software is pre-packaged.
- AMI are built for a specific region, and can be copied across regions.
- You can launch EC2 instances from

  - Public AMI: Provided by AWS
  - Your own AMI: You make and maintain them yourself.
  - AWS Marketplace AMI: An AMI someone else made, and potentially sells

- AMI Process
  - Start an EC2 instance and customize it
  - Stop the instance for data integrity
  - Build an AMI, which will also create EBS snapshots
  - Launch instances from other AMIs

### EC2 Image Builder

- Used to automate the creation of VMs or Container Images
  - Automatically build, test, and distribute AMIs
  - Example automated workflow for EC2 Image Builder:
    1. Creates a Builder EC2 instance that builds the components applied as specified on the recipe
    2. A New AMI is created out of this EC2 Instance
    3. A Test EC2 Instance is created, and test suite is run to ensure AMI is working
    4. AMI is distributed, possibly to multiple regions
- Can be run on a schedule specified by the user
- Free service
  - Pay only for the underlying resources ( EC2 Instances, storage for AMI, etc. )

### EC2 Instance Store

- EC2 Instance Store is a _high-performance hardware disk_ with better I/O performance than EBS volumes
- EC2 Instance Store lose their storage if they are stopped ( Ephemeral storage )
  - Risk of data loss if hardware fails
  - Backups and Replications are your responsibility
  - Good for buffer / cache / scratch data / temporary content

### Elastic File System (EFS)

- Managed _network file system_ that can be mounted on multiple EC2
  - Usually 100s of EC2s
  - Instances that mount the same EFS drive, using the EFS Mount Target, will be able to see the same files in EFS
- EFS works with _Linux_ EC2 instances
  - Can work across multiple Availability Zones
  - Highly available
  - Highly scalable
  - Very expensive, and metered payment
  - No capacity planning

#### EFS Infrequent Access (EFS-IA)

- Storage class that is cost-optimized for files not accessed every day.
- Heavily discounted cost compared to EFS standard
- EFS will automatically move your files to EFS-IA based on the last time they were accessed.
  - Determined by a Lifecycle Policy
  - e.g. Lifecycle Policy: Move files that are not accessed for 60 days to EFS-IA
- Transparent to the applications accessing EFS.
  - Behind-the-scenes cost optimization done by Amazon

### Shared Responsibility Model for EC2 Storage

| AWS                                               | User                                               |
| ------------------------------------------------- | -------------------------------------------------- |
| Infrastructure                                    | Setting up backup/snapshot procedures              |
| Replication for data for EBS volumes & EFS drives | Setting up data encryption                         |
| Replacing faulty hardware                         | Responsibility of any data on the drives           |
| Ensuring employees cannot access your data        | Understanding the risk of using EC2 Instance Store |

### Amazon FSx

- Launch 3rd party _high-performance file systems_ on AWS
- Fully managed by AWS

#### Amazon FSx for Windows File Server

- Highly reliable, and scalable Windows native shared file system.
- Built on Windows File Server
- Integrated with Microsoft Active Directory for user security.
- Can be accessed from AWS or your on-premise infrastructure.

#### Amazon FSx for Lustre

- Fully managed, high-performance, scalable file storage for _High Performance Computing_
  - Good for ML, Analytics, Video Processing, Financial Modelling
  - Scales up to 100s GB/s, millions of IO/s, sub-ms latencies

## Elastic Load Balancing & Auto-Scaling Groups

### Technical Terms: Availability, Scalability and Elasticity, Agility

#### Availability

- High availability means running your application / system in at least 2 AZs.
- The goal of high availability is to survive a data center loss, either to natural disasters or power outages.
- High availability usually goes hand in hand with horizontal scaling.

#### Scalability

- Scalability means that an application / system can handle greater loads by adapting
- Vertical Scalability

  - Increasing the size of the instance.
  - Very common for non-distributed systems, such as a database
  - Vertical scaling is limited by the hardware

- Horizontal Scalability
  - Increasing the number of instances / systems for your application
  - Very common for distributed systems, such as web applications
  - Easy to scale horizontally thanks to the cloud offerings such as Amazon EC2

#### Elasticity

- Once a system is scalable, there will be some _auto-scaling_ so that the system can scale based on the load.
- Complements the metered-payment cloud services very well.

#### Agility

- Reduced time to make resources available to developers.
- Cloud : New IT resources are only a click away.

### Load Balancers, and the Elastic Load Balancer

#### Load Balancer

- Servers that forward internet traffic to multiple services ( EC2 Instances ) downstream
- Spread load across multiple downstream instances
- Expose a single point of access ( DNS ) to your application
- Seamlessly handle failures of downstream instances
- Do regular health checks to your instances
- Provide SSL termination ( HTTPS ) for your websites.
- High availability across zones.

#### Elastic Load Balancer (ELB)

- Managed load balancer by AWS
  - AWS guarantees that it will be working
  - AWS takes care of upgrades, maintenance, high availability
  - AWS provides only a few configuration knobs
- It is less expensive to setup load balancer on your own, but it will take a lot more effort on your end.
- 4 kinds of load balancers offered by AWS
  - Application Load Balancer _(Layer 7)_
    - For HTTP / HTTPS only traffic
    - Static DNS (URL)
  - Network Load Balancer _(Layer 4)_
    - _Ultra-high performance_, allows for TCP and UDP only
    - Millions of requests per seconds, while maintaining ultra-low latency
    - Static IP through Elastic IP
  - Gateway Load Balancer _(Layer 3)_
    - GENEVE Protocol on IP Packets
    - Use Case: Route Traffic to Firewalls that you manage on EC2 Instances
    - Balances the load of the traffic to the virtual appliances that we run the EC2 Instances so that you can analyze the traffic or perform Firewall operations.
    - Traffic then sent back to the Gateway Load Balancer after analyzing the traffic.
    - The traffic is then forwarded to the Application.
  - Classic Load Balancer _(Layers 4 & 7)_
    - _To be replaced_ by the Application Load Balancer and Network Load Balancer in 2023.

### Auto-Scaling Group (ASG)

- Ensures cost effectiveness by running at optimal capacity.
  - Scales out to match an increased load.
  - Scales in to match a decreased load.
- Ensure we have a minimum and maximum number of machines running.
  - Minimum and maximum size specified by the user
- Automatically register new instances to a load balancer.
- Detect and replace unhealthy instances automatically.

#### Scaling Strategies

- Manual Scaling - Update the size of an ASG manually
- Dynamic Scaling - Respond to changing demand
  1. Simple / Step Scaling
     - When a CloudWatch alarm is triggered, then add 2 units / remove 1 unit.
  2. Target Tracking Scaling
     - Set the average ASG CPU to stay at around a target value.
  3. Scheduled Scaling
     - Anticipate a scaling based on known usage patterns
     - Increasing the capacity at certain timings
  4. Predictive Scaling
     - Uses ML to predict future traffic ahead of time.
     - Automatically provisions the right number of EC2 instances in advance to the predicted period
     - Useful when your load has predictable time-based patterns

## Amazon S3

- Advertised as an _infinitely scaling storage_
- Amazon S3 Use Cases
  - Backup and storage
  - Disaster Recovery
  - Archive
  - Hybrid Cloud storage
  - Application hosting
  - Media hosting
  - Data lakes and Big Data Analytics
  - Software Delivery
  - Static website

### Amazon S3 Buckets

- S3 allows people to store _objects_ (files) in _buckets_ (directories)
- Buckets must have a globally unique name across all regions and all accounts
- S3 is a global service, but the buckets are created in a region.
- Naming Convention for buckets:
  - No uppercase, No underscore
  - 3-63 characters long
  - Not an IP
  - Must start with lowercase letter or number
  - Must not start with the prefix `xn--`
  - Must not end with the suffix `-s3alias`

### Amazon S3 Objects

- Each object has a key.
- The key is composed of `prefix` + `object name`
- There are no concept of _directories_ within buckets, just keys with very long names that contain slashes ( `/` ).
- The key is the full path to the object
  - e.g. `s3://my-bucket/my_file.txt`
  - e.g. `s3://my-bucket/another_folder/my_file.txt`
- Each object value contains
  - Metadata
    - List of text key / value pairs
    - System or user metadata
  - Tags
    - Unicode key / value pair, up to 10
    - Useful for security / lifecycle
  - Version ID
    - Only present if versioning is enabled.
  - Value
    - Content of the body.
    - Maximum object size is 5TB
    - If uploading more than 5GB, must use `multi-part upload`.

### Amazon S3 Security

#### Types of S3 Securities

- User-Based
  - IAM Policies
    - Which API calls should be allowed for a specific user from IAM
    - An IAM principal can access an S3 object if all of the following conditions are met:
      - The user IAM permissions _or_ the resource policy _allows_ it
      - There is no explicit _deny_ in the action
- Resource-Based
  - Bucket Policies
    - Bucket-wide rules from the S3 console, which is applied across accounts
    - Object Access Control List (ACL)
    - Bucket Access Control List (ACL)
- Encryption
  - Encrypt objects in Amazon S3 using encryption keys.

#### S3 Bucket Policies

- JSON based policies
  - Resources: Buckets and Objects
  - Effect: Allow / Deny
  - Actions: Set of API to Allow / Deny
  - Principal : Account or user to apply the policy to
- Use S3 bucket for policy to:
  - Grant public access to the bucket
  - Force objects to be encrypted at upload
  - Grant access to another account
- Bucket settings for Block Public Access
  - Should only be disable if you want to set your own public bucket policy.
  - Used to prevent company data leaks
  - If you know your bucket should never be public, leave these on.
  - Can be set at the account level.

### S3 Static Website Hosting

- S3 can host static websites and have them accessible on the Internet.
  - Website URL created depends on the region.
- If a `403 Forbidden Error` is thrown when you enter the URL, make sure the bucket policy allows public reads.

### S3 Versioning

- Enabled at the bucket level
- Same key overwrite will change the version number.
  - Protect against unintended deletes (Ability to restore a version)
  - Easy roll back to previous version
- Any file that is not versioned prior to enabling versioning will have version `null`
- Suspending versioning does not delete the previous versions

### S3 Replication

- Must enable Versioning in source and destination buckets
- Buckets can be in different AWS accounts
- Copying is asynchronous
- Must be given proper IAM permissions to S3 to do replication
- Cross-Regional Replication
  - Regions must be different
  - Useful for compliance, lower latency access across regions, and replication across accounts
- Same-Regional Replication
  - Regions must be the same
  - Useful for log aggregation, live replication between production and test accounts so that we have our own test environment.

### S3 Storage Classes

When we define our objects, we choose its storage class.

- Amazon S3 Lifecycle configurations
  - Defined by the user
  - Automatically moves objects across the different storage classes after a period of time has passed.

#### Durability and Availability

- High durability means that we can expect to incur loss of a single object with a very low probability.
- Availability measures how readily available a service is.
  - S3 has 99.99% availability, meaning that the service is unavailable 53 minutes a year.

#### S3 Standard - General Purpose

- 99.99% Availability
- Used for frequently accessed data
- Low latency and high throughput
- Sustain 2 concurrent facility failures on the side of AWS
- Use Cases: Big Data Analytics, Mobile & Gaming Applications, Content Distribution, etc.

#### S3 Infrequent Access (IA) Storage Classes

- For Data that is less frequently accessed, but requires rapid access when needed
- Lower cost than S3 Standard, but there is a cost-on-retrieval

- S3 Standard - Infrequent Access
  - 99.9% Availability
  - Use Cases: Disaster Recovery, Backups
- S3 One Zone - Infrequent Access
  - 99.5% Availability
  - Extremely high durability (Almost 100%) in a single AZ
  - Data lost when AZ is destroyed
  - Use Cases: Storage secondary backup copies of on-premise data, or re-creatable data.

#### S3 Glacier Storage Classes

- Low-cost object storage meant for archiving / backup
- Pricing Scheme
  - Price for storage
  - Object retrieval cost
- Amazon S3 Glacier Instant Retrieval
  - Millisecond retrieval
  - Great for data accessed once a quarter
  - Minimum storage duration of 90 days
- Amazon S3 Glacier Flexible Retrieval
  - Formerly known as Amazon S3 Glacier
  - Three levels of retrieval time
    1. Expedited : 1~5 minutes
    2. Standard : 3~5 hours
    3. Bulk: 5~12 hours (free)
  - Minimum storage duration of 90 days
- Amazon S3 Glacier Deep Archive
  - Two levels of retrieval time
    1. Standard: ~12 hours
    2. Bulk: ~48 hours
  - Minimum storage duration of 180 days

#### S3 Intelligent-Tiering

- Small monthly monitoring and auto-tiering fee
- Moves objects automatically between Access Tiers based on usage
- There are _no_ retrieval charges in S3 Intelligent-Tiering
- Tiers that are configurable under Intelligent-Tiering:
  1. Frequent Access tier : Default tier
  2. Infrequent Access tier: Objects not accessed for 30 days
  3. Archive Instant Access tier: Objects not accessed for 90 days
  4. Archive Access tier: Configurable from 90 days to 700+ days _(Optional)_
  5. Deep Archive Access tier: Configurable from 180 days to 700+ days _(Optional)_

### S3 Encryption

- Server-side Encryption
  - Server encrypts the file after receiving it
  - Always active
- User-side Encryption
  - User encrypts the file before uploading it

### Shared Responsibility Model for S3

| AWS                                      | User                                   |
| ---------------------------------------- | -------------------------------------- |
| Infrastructure                           | S3 Versioning                          |
| Configuration and Vulnerability Analysis | S3 Bucket Policies                     |
| Compliance Validation                    | S3 Replication Setup                   |
|                                          | Logging and Monitoring                 |
|                                          | S3 Storage Classes                     |
|                                          | Data encryption at rest and in transit |

### AWS Snow Family

- Highly-secure, physical, portable devices to:
  1. Collect and process data at the edge
  2. Migrate data into and out of AWS
- Data migration
  1. Snowcone
  2. Snowball Edge
  3. Snowmobile
- Edge Computing
  1. Snowcone
  2. Snowball Edge

#### Data Migrations with AWS Snow Family

- If it takes more than a week to transfer data over the network, it is advisable to use Snowball devices
- Targets the following challenges:
  1. Limited connectivity
  2. Limited bandwidth
  3. High network cost
  4. Shared bandwidth - Cannot maximize the line
  5. Connection stability
- Usage Process:
  1. Request AWS snow device from the AWS console for delivery
  2. Install the client / AWS OpsHub on your server.
  3. Connect the snowball to your servers and copy files using the client
  4. Ship the device back to AWS when you are done.
  5. Data will be loaded into an S3 bucket
  6. Snow device is completely wiped

#### Snowball Edge

- Physical data transport solution
  - Move TBs or PBs of data in or out of AWS
- Alternative to moving data over the network
- Pay per data transfer job
- Provide block storage and Amazon S3-compatible object storage
- Two types of Snowball Edge devices
  1. Snowball Edge Storage Optimized
  2. Snowball Edge Compute Optimized
- Use Cases:
  - Large data cloud migrations
  - DC decommission
  - Disaster recovery

#### Snowcone

- Small, light
- Portable computing
- Rugged and Secure
- Can withstand harsh environments
- Must provide your own batteries / cables
- Can be sent back to AWS offline, or connect it to the internet, and use AWS DataSync to send data.
- Two types of Snowcone device
  1. Snowcone
     - 8 TB of HDD Storage
  2. Snowcone SSD
     - 14 TB of SSD Storage
- Use Cases:
  - Edge Computing
  - Storage and data transfer in space-constrained environments
    - Where the Snowball Edge does not fit.

#### Snowmobile

- An actual truck, which can help with transferring up to exabytes of data
- Each Snowmobile has 100PB of capacity
  - Can use multiple Snowmobiles in parallel
- High security
  - Temperature-controlled
  - GPS
  - 24/7 video surveillance
- Better than Snowball if you transfer more than 10PB of data

#### Edge Computing

- Process data while it is being created on an edge location
  - A truck on the road
  - A ship on the sea
  - A mining station underground
- These locations may have:
  - Limited to no internet access
  - Limited to no easy access to computing power
- We can setup a Snowball Edge / Snowcone device to do edge computing
  - All of these devices can run EC2 Instances & AWS Lambda functions using AWS IoT Greengrass
  - Long-term deployment options are available:
    - Borrow for 1 or 3 years at discounted pricing
- Use Cases of Edge Computing:
  - Pre-process data
  - Machine learning at the edge
  - Transcoding media streams
- Eventually, we can ship back the device to AWS for storage

#### AWS OpsHub

- A software to be installed on your computer / laptop to manage your Snow Family Device through a GUI
  - Unlocking and configuring single or clustered devices
  - Transferring files
  - Launching and managing instances running on Snow Family Devices
  - Monitor device metrics
    - Storage capacity
    - Active instances on your device
  - Launch compatible AWS services on your devices
    - Amazon EC2 instances
    - AWS DataSync
    - Network File system

### Hybrid Cloud for Storage

- Part of your infrastructure is on-premises
- Part of your infrastructure is on the cloud
- This can be due to
  - Long cloud migrations
  - Security requirement
  - Compliance requirement
  - IT strategy
- S3 is a proprietary storage technology, so we expose the S3 data on-premise using the AWS Storage Gateway

### AWS Storage Gateway

- Bridge between on-premise data and cloud data in S3
- Hybrid storage service to allow on-premises to seamlessly use the AWS Cloud
- Use Cases
  - Disaster recovery
  - Backup & Restore
  - Tiered storage
- Types of Storage Gateway
  1. File Gateway
  2. Volume Gateway
  3. Tape Gateway

## Databases & Analytics

### Databases Introduction

- Storing data on disk can have its limits
- Sometimes, you want to store data in a database
  - Structure the data
  - Build indexes to efficiently query the data
  - Define relationships between your datasets
- Databases are optimized for a purpose and come with different features, shapes and constraints.

#### Relational Databases

- Table-structured
- Can use the SQL language to perform queries / lookups

#### NoSQL Databases

- NoSQL databases are purpose-built for specific data models and have flexible schemas for building modern applications
- Benefits of using NoSQL over Relational Databases
  - Flexibility: Easy to evolve data model
  - Scalability: Designed to scale-out by using distributed clusters
  - High-performance: Optimized for a specific data model
  - Highly functional: Types optimized for the data model

#### Databases and Shared Responsibility

| AWS                                                | User                |
| -------------------------------------------------- | ------------------- |
| Quick provisioning, High availability, Scaling     | Input data to store |
| OS Patching                                        |                     |
| Monitoring, alerting                               |                     |
| Automated Backup and Restore, Operations, Upgrades |                     |

- Note that you can run your own database technology on EC2, but you must handle the resiliency, backup, patching, high availability, fault tolerance, scaling, etc.

### AWS Relational Database Service (RDS) Overview

- Managed Database service, using SQL as a query language
- Allows users to create databases in the cloud that are managed by AWS using
  - Postgres
  - MySQL
  - MariaDB
  - Oracle
  - Microsoft SQL Server
  - Aurora (AWS Proprietary database)

#### Advantage over using RDS versus deploying DB on EC2

- RDS is a managed service
  - Automated provisioning, OS patching
  - Continuous backups and restore to specific timestamp
    - Point in Time Restore
  - Monitoring dashboards
  - Read replicas for improved read performance
  - Multi-AZ setup for Disaster Recovery
  - Maintenance windows for upgrades
  - Vertical and horizontal scaling capability
  - Storage backed by EB2
    - _gp2_
    - _io1_
- Only downside: you cannot SSH into your AWS RDS instances

#### RDS Deployments

- Read Replicas
  - Scale the read workload of your DB
  - Can create up to 15 Read Replicas
  - Data is only written to the main DB
- Multi-AZ
  - Failover is triggered in case of AZ outage, and application will failover to the failover database.
  - Data is only read / written to the main database
  - Can only have 1 other AZ as failover
- Multi-Region
  - For Read Replicas only
    - Local performance for global reads
    - Data is written only to the main DB
  - Disaster recovery in case of region issue
  - Replication cost

### AWS Aurora

- An _AWS-implementation_ of PostgreSQL / MySQL
- Aurora is a proprietary technology from AWS
  - Not open-sourced
  - Not in free tier
  - Aurora costs more than RDS (20% more), but is more efficient
- Aurora is _AWS cloud optimized_ and claims 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
- Aurora storage automatically grows in increments of 10GB, up to 128TB

### DocumentDB

- An _AWS-implementation_ of MongoDB
  - Store, query, and index JSON data
- Fully-managed, highly available with replication across 3 AZ
- Automatically scales to workloads with millions of requests per seconds.
- Storage automatically grows in increments of 10GB, up to 64TB

### Amazon ElastiCache

- Manages Redis or Memcached
  - Caches are _in-memory_ databases with high performance, and low latency
- Helps reduce load off databases for read-intensive workloads
- AWS takes care of:
  - OS maintenance / patching
  - Optimizations
  - Setup
  - Configuration
  - Monitoring
  - Failure recovery
  - Backups

### DynamoDB

- Fully-managed highly available database with replication across 3 AZ
  - Key/Value NoSQL Database
- Scales to massive workloads, distributed _serverless_ database.
  - Millions of requests per seconds, trillions of rows, 100s of TB of storage
  - Fast and consistent in performance
  - Single-digit millisecond latency
- Integrated with IAM for security, authorization and administration
- Low cost, and auto-scaling capabilities

#### DynamoDB Accelerator - DAX

- Fully-managed in-memory cache for DynamoDB
- 10x performance improvement when accessing DynamoDB tables
  - Single-digit millisecond latency to microseconds latency
- Secure, highly scalable and highly available
- Difference with ElastiCache:
  - DAX is only used for and is integrated really well with DynamoDB
  - ElastiCache can be used for other databases

#### DynamoDB - Global Tables

- Makes a DynamoDB table accessible with low latency in multiple regions
- Active-Active replication
  - Read / Write to any AWS Region

### Redshift

- Based on PostgreSQL, but it is not used for Online Transaction Processing (OLTP)
- Online Analytical Processing (OLAP)
  - Analytics and Data Warehousing
- Load data once every hour, not every second
- 10x better performance than other data warehouses, scales to PBs of data.
- Columnar storage of data
  - Instead of row-based
- Massively Parallel Query Execution, Highly available
- Pay-as-you-go based on the instances provisioned
- Has a SQL interface for performing the queries
- Business Intelligence tools such as AWS Quicksight or Tableau integrate with it.

### Amazon Elastic MapReduce (EMR)

- EMR helps creating Hadoop clusters to analyze and process vast amount of data
- Clusters can be made of 100s of EC2 instances
- Supports Apache Spark, HBase, Presto, Flink, etc.
- EMR takes care of all the provisioning and configuration
- Auto-scaling and integrated with Spot instances
- Use Cases:
  - Data processing
  - Machine Learning
  - Web indexing
  - Big Data

### Amazon Athena

- Serverless query service to analyze data stored in Amazon S3
- Built on the Presto engine
- Use standard SQL language to query the files
- Supports CSV, JSON, ORC, Avro, Parquet
- Use compressed or columnar data for cost-savings
  - $5 per TB of data scanned
  - Less scanning required
- Use Cases:
  - Business Intelligence
  - Business Analytics
  - Business Reporting
  - Analyze and Query Virtual Private Cloud (VPC) Flow Logs
  - ELB Logs
  - CloudTrail trails

### Amazon Quicksight

- Serverless machine learning-powered business intelligence service to create interactive dashboards
- Fast, automatically scalable, embed-able, with per-session pricing
- Integrated with other services such as RDS, Aurora, Athena, Redshift, S3
- Use Cases:
  - Business Analytics
  - Building visualizations
  - Perform ad-hoc analysis
  - Get business insights using data

### Amazon Neptune

- Fully-managed graph NoSQL database
  - Build and run applications working with highly connected datasets - Optimized for these complex and hard queries.
  - Can store up to billions of relations and query the graph with milliseconds latency
- Highly available across 3 AZ, with up to 15 read replicas.
- Great for knowledge graphs, fraud detection, recommendation engines, social networking, etc.

### Amazon Managed Blockchain

- Blockchain makes it possible to build applications where multiple parts can execute transactions without the need for a trusted, central authority.
- Managed service to
  - Join public blockchain networks
  - Create your own scalable private network
- Compatible with the frameworks Hyperledger Fabric & Ethereum

### Amazon Quantum Ledger Database (QLDB)

- A ledger is a book recording financial transactions
- Fully-managed, Serverless, highly available, replication across 3 AZ
- Used to review history of all the changes made to your application data over time
- Immutable System
  - No entry can be removed or modified, cryptographically verifiable
- Better performance than common ledger blockchain frameworks, manipulate data using SQL.
- Difference with Amazon Managed Blockchain: No decentralization component, in accordance with financial regulation rules.

### AWS Glue

- Managed extract, transform, and load (ETL) service
  - Useful to prepare and transform data for analytics
- Fully serverless service
  - Only need to worry about actual data transformation
- Glue Data Catalog
  - Catalog of datasets
  - Can be used by Athena, Redshift, EMR

### Database Migration Service (DMS)

- Quickly and securely migrate databases to AWS
- Resilient and Self-healing
- The source database remains available during the migration
- Supports both Homogeneous and heterogeneous migrations
  - Homogenous: Source and target database are the same
  - Heterogeneous: Source and target database are different

### Databases & Analytics Summary

| Requirement                               | AWS                       |
| ----------------------------------------- | ------------------------- |
| In-memory Database                        | ElastiCache               |
| Relational Databases - OLTP               | RDS & Aurora (SQL)        |
| Relational Databases - OLAP               | Redshift (SQL)            |
| Aurora for MongoDB                        | DocumentDB                |
| Key/Value Database                        | DynamoDB & DAX            |
| Graph Database                            | Neptune                   |
| Hadoop Cluster                            | EMR                       |
| Query data on Amazon S3                   | Athena                    |
| Dashboards on your data                   | QuickSight                |
| Financial Transactions Ledger             | Amazon QLDB               |
| Hyperledger Fabric & Ethereum blockchains | Amazon Managed Blockchain |
| Managed ETL and Data Catalog              | Glue                      |
| Database Migration                        | DMS                       |

## Other Compute Services: ECS, Lambda, Batch, Lightsail

### Elastic Container Service (ECS)

- Launch Docker containers on AWS
- Must provision and maintain the infrastructure (EC2 Instances)
  - AWS takes care of starting / stopping containers
  - Has integrations with the Application Load Balancer

### Fargate

- Launch Docker containers on AWS
- Do not need to provision the infrastructure (No EC2 Instances)
  - Serverless offering
  - AWS just runs containers for you based on the CPU / RAM you need

### Elastic Container Registry

- Private Docker Registry on AWS
- This is where you store your Docker images
  - Fargate / ECS looks at the images and creates the containers

### Lambda

- Virtual functions, no servers to manage
- Limited by time, short executions
  - Invocation time: Up to 15 minutes
- Run on-demand
  - Pay per request and compute time
  - Free tier of a million AWS Lambda requests, and 400,000GBs of compute time
- Scaling is automated
- Integrated with the whole AWS suite of services
- Event-Driven: Functions get invoked by AWS when needed
- Easy monitoring through AWS CloudWatch
- Easy to get more resources per function
  - Up to 10GB of RAM
  - Increasing RAM will also improve CPU and network
- Fully integrated with many programming languages
- Can also run container images
  - The container image must implement the Lambda Runtime API
  - ECS / Fargate are still preferred for running arbitrary Docker images
- Use Cases:
  - Serverless thumbnail Creation
  - Serverless CRON job

### API Gateway

- Fully-managed service for developers to easily create, publish, maintain, monitor, and secure APIs
- Serverless and scalable
- Supports RESTful APIs and WebSocket APIs
- Support for security, user authentication, API throttling, API keys, monitoring, etc.

### AWS Batch

- Fully-managed batch processing at _any scale_
  - A batch job is a job with a start and an end
  - Unlike Lambda, AWS Batch has no time limit.
  - Helpful for cost optimizations and focusing less on the infrastructure
  - You submit / schedule batch jobs, and AWS Batch does the rest.
- Batch jobs are defined as docker images and run on ECS
- Efficiently run 100,000s of computing batch jobs on AWS
  - Batch will dynamically launch EC2 instances or Spot Instances to run the batch jobs
  - AWS Batch provisions the right amount of computation and memory

### Amazon Lightsail

- Virtual servers, storage, databases, and networking
- Low and predictable pricing
- Simpler alternative to using EC2, RDS, ELB, EBS, Route 53, etc.
- Great for people with little cloud experience
- Can setup notifications and monitoring of your Lightsail resources
- Has high availability but no auto-scaling, and has limited AWS integrations.
- Use Cases:
  - Simple web applications
  - Websites
  - Dev / Test environment

## Deploying and Managing Infrastructure at Scale

### AWS Cloud Formation

- Declarative way of outlining your AWS infrastructure for any resources
  - Supports almost all AWS resources
  - Can use _custom resources_ for resources that are not supported
  - Creates infrastructure for you in the right order, with the exact configuration that you specify
- Infrastructure as code
  - No resources are manually created, which is excellent for control
  - Changes to infrastructure are reviewed through code
- Estimable costs for resources using CloudFormation template
  - Each resource within the stack is tagged with an identifier so you can easily see how much a stack costs you.
  - An example savings strategy is to automate the deletion of templates at 5PM and recreate it at 8AM safely.
- Productivity
  - Ability to destroy and re-create an infrastructure on the cloud on the fly.
  - Automated generation of diagram for your templates
  - Declarative programming
    - No need to figure out ordering and orchestration
- Leverage on existing templates on the web

#### CloudFormation Stack Designer

- We can see all the resources
- We can see all the relations between components

### AWS Cloud Development Kit (CDK)

- Define cloud infrastructure using a familiar language instead of _JSON / YAML_ format
  - JavaScript / TypeSCript
  - Python
  - Java
  - .NET
- Code is compiled into a CloudFormation template _( JSON / YAML )_
  - Can deploy infrastructure and application runtime code together
  - Great for Lambda function
  - Great for Docker Containers in ECS / EKS

### Developer problems on AWS

- Managing infrastructure
- Deploying code
- Configuring all the databases, load balancers, etc.
- Scaling concerns
- Most web applications have the same architecture _( ALB + ASG )_
- All developers want is for their code to run
  - Possibly, consistently across different applications and environments

### AWS Elastic Beanstalk

- Managed service
  - Just the application code is the responsibility of the developer
    - Instance configuration / OS is handled by Beanstalk
    - Deployment strategy is configurable but performed by Elastic Beanstalk
    - Capacity provisioning
    - Load balancing & auto-scaling
    - Application health-monitoring & responsiveness
  - A developer-centric view of deploying an application on AWS
    - Full control over the configuration
  - Platform-as-a-Service
    - Free, but you pay for underlying resources
- Architecture models
  1. Single Instance Deployment
     - Good for development
  2. Load Balancing + Auto-Scaling Groups
     - Great for production or pre-production web application
  3. Auto-Scaling Groups only
     - Great for non-web applications in production
- Support for many platforms
  - Python, PHP, Ruby, Node.js, Go

#### Elastic Beanstalk - Health Monitoring

- Health agent pushes metrics to CloudWatch
  - Checks for application health, publishes health events

### AWS CodeDeploy

- Deploy applications automatically
  - Hybrid service
    - Works with EC2 Instances
    - Works with On-Premises Servers
- Servers and Instances must be provisioned and configured ahead of time with the CodeDeploy Agent

### AWS CodeCommit

- AWS' competing product against GitHub
  - Fully managed, scalable and highly available
  - Private, Secured, and Integrated with AWS
- Source-control service that hosts Git-based repositories
- Makes it easy to collaborate with others on code
- Code changes are automatically versioned

### AWS CodeBuild

- Code building service in the cloud
- Compiles source code, run tests, and produces packages that are ready to be deployed
- Fully managed, and serverless
  - Continuously scalable and highly available
  - Secure
  - Pay-as-you-go pricing - Only pay for the build time

### AWS CodePipeline

- Orchestrate the different steps to have the code automatically pushed to production.
  - Code => Build => Test => Provision => Deploy
  - Basis for CI/CD
- Fully managed
  - Fast Delivery and rapid updates
  - Compatible with:
    - Other AWS Services
    - 3rd-party services such as GitHub
    - Custom plug-ins

### AWS CodeArtifact

- The storing and retrieving of software dependencies is called artifact management.
- AWS CodeArtifact is a secure, scalable, and cost-effective artifact management for software development.
- Works with common dependency management tools
  - Maven
  - Gradle
  - npm
  - yarn
  - twine
  - pip
  - NuGet
- Developers and CodeBuild can retrieve dependencies straight from CodeArtifact

### AWS Cloud9

- Cloud IDE for writing, running and debugging code
  - Used within a web browser
    - Can work from office, home, or anywhere with internet with no setup necessary
  - Allows for pair programming

### AWS CodeStar

- Unified user interface to easily manage software development activities in one place
- Quick way to get started to correctly set-up CodeCommit, CodePipeline, CodeBuild, CodeDeploy, Elastic Beanstalk, EC2, etc.
- Can edit the code _in-the-cloud_ using AWS Cloud9

### AWS Systems Manager (SSM)

- Manages EC2 and On-Premises systems at scale
  - Hybrid AWS Service
- Get operational insights about the state of your infrastructure
- Suite of 10s of products
  - Patch automation for enhanced compliance
  - Run commands across an entire fleet of servers
  - Store parameter configuration with the SSM Parameter Store
- Works for Linux, Windows, MacOS, and Raspberry Pi OS

#### How SSM works

- SSM Agent need to be installed onto the system we control.
  - Installed on Amazon Linus AMI & some Ubuntu AMIs by default.
  - SSM Agent helps us with running commands, patching and configuring our servers.
- If an instance cannot be controlled with SSM, it is probably an issue with the SSM agent.

#### SSM Session Manager

- Allows you to start a secure shell on your EC2 and on-premises server
  - Without having ssh access, bastion hosts, or ssh keys.
  - Without requiring _port 22_.
    - EC2 Instance has a SSM Agent, which is connected to the Session Manager service
    - Very secure
    - User can access through the Session Manager service, and execute commands on it.
  - Supports Linux, macOS, and Windows.
- Sends session log data to S3 or CloudWatch Logs.

### AWS OpsWorks

- AWS' handled Chef & Puppet
- Only reason why you should use OpsWorks is because you are already using Chef & Puppet before migrating to the cloud.
  - If you want to re-use your Chef & Puppet template.
- Automation platform that allows you to use code to automate the configurations of your server
  - Work great with EC2 and On-Premises VM
  - Alternative to AWS SSM
  - Only provision standard AWS resources

## Leveraging the AWS Global Infrastructure

### Global Applications

#### Advantages of Global Applications

- A global application in an application deployed in multiple geographies
  - These multiple geographies can be region / edge Locations in AWS
- Decreased Latency
  - Latency is the time it takes for a network packet to reach a server
  - Deploy your applications closer to your users to decrease latency, and deliver a better user experience
- Disaster Recover
  - If an AWS region goes down, we can always fail-over to another region and have the application still working
  - Important to increase the availability of the application.
- Attack protection
  - Distributed global infrastructure is harder to attack.

#### Global AWS Infrastructure

- Regions: For deploying applications and infrastructure
- Availability Zones: Made of multiple data centers
- Edge Locations: For content delivery as close as possible to users

### Route 53

- Managed Domain Name System (DNS)
  - Great to route users to the closest deployment with least latency
  - Great for disaster recover strategies

#### Route 53 Routing Policies

1. Simple Routing Policy
   - Only routing policy without health checks.
2. Weighted Routing Policy
   - Distribute traffic across multiple EC2 instances with a specified weight.
3. Latency Routing Policy
   - Route users to the EC2 instances that provide the lowest latency.
4. Failover Routing Policy
   - Health check on primary EC2 instances to provide disaster recovery.

### CloudFront

- Content Delivery Network (CDN)
- Replicate part of your application to AWS Edge Locations
  - Decrease Latency
- Cache content at the edge locations
  - Improved user experience and decreased latency
- DDoS protection
  - Integration with Shield
  - AWS Web Application Firewall (WAF)
- CloudFront _Edge Locations_ will connect with your Origin
  - Once the result is retrieved, the result will be cached in the Edge Location

#### CloudFront - Origins

- S3 bucket
  - For distributing files and caching them at the edge locations
  - Enhanced security with CloudFront Origin Access Control (OAC)
  - CloudFront can be used as an ingress to upload files to S3
- Custom Origin (HTTP)
  - Application Load Balancer
  - EC2 Instance
  - S3 Website
  - Any HTTP backend you want

#### Comparison with S3 Cross Region Replication

| CloudFront                                                 | S3 Cross Region Replication                                                        |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Global Edge network                                        | Must be setup for each region we want the replication in                           |
| Files are cached for a TTL                                 | Files are updated in near real-time                                                |
| Great for static content that must be available everywhere | Great for dynamic content that needs to be available at low-latency in few regions |
|                                                            | Read only                                                                          |

### S3 Transfer Acceleration

- Accelerate global uploads and downloads into Amazon S3
  - Transfer file to an AWS edge location, which will forward the data to the S3 bucket in the target region

### AWS Global Accelerator

- Improve global application availability and performance using the AWS global network
- Leverage the AWS internal network to optimize the route to your application
- 2 Anycast IP are created
  - Application and traffic is sent through Edge Locations
  - Edge Locations send the traffic to your application

#### Comparison with CloudFront

- Similarities
  - Both use AWS global network and its edge locations around the world
  - Both services integrate with AWS Shield for DDoS protection
- CloudFront - Content Delivery Network
  - Improves performance for cache-able content
  - Content is served _at the edge_
- Global Accelerator
  - No caching, or proxying packets at the edge to applications running in one or more AWS regions
  - Improves performance for a wide range of applications over TCP or UDP
  - Good for HTTP use cases that require static IP addresses
  - Good for HTTP use cases that required deterministic fast regional failover

### AWS Outposts

- Server racks that offers the same AWS infrastructure, services, APIs and tools to build your own applications on-premise just as in the cloud.
  - Hybrid cloud
  - _Outpost Racks_ are pre-loaded with AWS services
- AWS will setup and manage _Outpost Racks_ within your on-premise infrastructure and you can start leveraging AWS services on-premises
  - Low-latency access to on-premises systems
  - Local data processing
  - Data residency
  - Easier migration from on-premises to the cloud
  - Fully manages services
- You are responsible for the physical security of your _Outpost Rack_.

### AWS WaveLength

- Wavelength Zones are infrastructure deployments embedded within the telecommunications providers' data centers at the edge of the 5G networks.
  - Brings AWS services to the edge of the 5G networks
  - Ultra-low latency applications through 5G networks
  - Traffic does not leave the Communication Service Provider's (CSP) network
  - High-bandwidth and secure connection to the parent AWS Region
  - No additional charges or services agreements
- Use Cases:
  - Smart Cities
  - ML-assisted diagnostics
  - Connected Vehicles
  - Interactive Live Video Streams
  - AR / VR
  - Real-time Gaming

### AWS Local Zones

- Places AWS compute, storage, database, and other selected AWS services closer to end users to run latency-sensitive applications.
- Extend your Virtual Private Cloud (VPC) to more locations
  - Extension of an AWS Region
- Compatible with EC2, RDS, ECS, EBS, ElastiCache, Direct Connect, etc.

## Cloud Integration

### Cloud Integration Overview

- When we start deploying multiple applications, they will inevitably need to communicate with one another.
- There are two patterns of application communication
  1. Synchronous communications
     - Application to application
  2. Asynchronous / Event-based
     - Application to queue to application
- Synchronous between applications can be problematic if there are sudden spikes of traffic
  - Better to decouple your applications using:
    1. SQS: Queue model
    2. SNS: Publisher / Subscriber model
    3. Kinesis: Real-time data streaming model
  - These services can scale independently from our application

### Amazon Simple Queue Service (SQS)

- Fully managed serverless service
  - Used to decouple applications
- Scales from 1 message per second to 10,000s per second
  - Low latency: <10ms on publish and receive
- No limit to how many messages can be in the queue
  - Messages are deleted after they are read by customers
  - Consumers share the work to read messages and scale horizontally.
- Default retention of messages: 4 days, maximum of 14 days

### Amazon SNS

- Sending one message to many receivers
  - Event publishers only send message to one SNS topic
  - As many event subscribers as we want to listen to the SNS topic notifications
  - Each subscriber to the topic will get all the messages.
- No message retention

### Amazon Kinesis

- For real-time big data streaming
- Managed service to collect, process, and analyze real-time streaming data at _any scale_

### Amazon MQ

- Amazon MQ is a managed message broker service for:
  - RabbitMQ
  - ActiveMQ
- Does not scale as much as SQS / SNS
- Amazon MQ runs on servers, can run in Multi-AZ with failover
- Amazon MQ has both queue feature (SQS) and topic features (SNS)

## Cloud Monitoring Services

### Amazon CloudWatch

#### Amazon CloudWatch Metrics

- A metric is a variable to monitor
  - Metrics have timestamps
  - Example metrics:
    1. EC2 Instances
    2. EBS Volumes
    3. S3 Buckets
    4. Billing
    5. Service Limits
    6. Custom Metrics
- CloudWatch provides metrics for every services in AWS
- Can create CloudWatch dashboards of metrics

#### Amazon CloudWatch Alarms

- Alarms are used to trigger notifications for any metric
- Alarm actions
  - Auto-Scaling
    - Increase / Decrease EC2 instances' "desired" count
  - EC2 Actions
    - Stop, terminate, reboot or recover an EC2 Instance
  - SNS Notifications
    - Send a notification into an SNS topic
- Can choose the period on which to evaluate an alarm
- Alarm States:
  1. OK
     - The metric or expression is outside of the defined threshold.
  2. INSUFFICIENT_DATA
     - The metric or expression is within the defined threshold.
  3. ALARM
     - The alarm has just started or not enough data is available.

#### Amazon CloudWatch Logs

- Enable real-time monitoring of logs
- Adjustable CloudWatch Logs retention
- By default, no logs from your EC2 instance will go to CloudWatch
  - You will need to run a CloudWatch agent on EC to push the log files you want
  - Make sure IAM permissions are correct
  - The CloudWatch log agent can be setup on-premises too

### Amazon EventBridge

- React to events in AWS, or trigger a rule on a schedule
  - Schedule CRON jobs
  - Event rules to react to a service doing something
  - Trigger Lambda functions, send SQS/SNS messages
- Event Buses
  - Default Event Bus: Events happening from within AWS Services.
  - Partner Event Bus: Events happening from partners of AWS.
  - Custom Event Bus: Events happening from custom applications.
- Schema Registry
  - Model the event schema ( See what the data looks like )
- You can archive events sent to an event bus
  - Ability to replay archived events

### Amazon CloudTrial

- Provides governance, compliance, and audit for your AWS Account
- Enabled by default
- Get an history of events / API calls made within your AWS Account through
  1. Console
  2. SDK
  3. CLI
  4. AWS Services
- Can put logs from CloudTrial into CloudWatch Logs or S3.
- A trail can be applied to All Regions or a single Region
- If a resource is deleted in AWS, investigate the CloudTrail first

#### CloudTrail Insights

- Provides automated analysis of your CloudTrail Events

### AWS X-Ray

- Trace and get visual analysis of your own application
- Helps troubleshoot performance and identify bottlenecks
  - Find if we are meeting our Service Level Agreement (SLA)
  - Find places where we are throttled
  - Identify users that are impacted
- Understand dependencies in a microservice architecture
- Pinpoint service issues
  - Review request behavior
  - Find errors and exceptions

### Amazon CodeGuru

- Machine Learning-powered service
- CodeGuru Reviewer
  - Trained by lessons across millions of code reviews on 1000s of open-source and Amazon repositories
  - Automated code reviews for static code analysis
  - Identify critical issues, security, vulnerabilities, and hard-to-find bugs.
  - Supports strictly Java and Python, and integrates with GitHub, Bitbucket, and AWS CodeCommit
- CodeGuru Profiler
  - Helps understand the runtime behavior of your application
  - Visibility / recommendations about application performance during runtime.
    - Identify and remove code inefficiencies
    - Improve application performance
    - Decrease computational costs
    - Provides heap summary
    - Anomaly detection
  - Supports applications running on AWS or on-premise
  - Minimal overhead on application
  
### AWS Health Dashboard

Global Service that monitors the health of your services.

1. Service History
   - Shows all regions, all services health
   - Shows historical information for each day
2. Your Account
   - Provides alerts and remediation guidance when AWS is experiencing events that may impact you.
   - Gives you a personalized view into the performance and availability of the AWS services underlying your AWS resource
   - Displays relevant and timely information to help you manage events in progress, and provides proactive notification to help you plan for scheduled activities
   - Can aggregate data from an entire AWS Organization

## VPC & Networking

### IP Addresses in AWS

- Internet Protocol version 4 (IPv4)
  - Private IPv4 is fixed for EC2 instances even if you start/stop them.
  - EC2 instance gets a new public IP address every time you stop then start it.

- Elastic IP
  - Allows you to attach a fixed public IPv4 address to EC2 instance
  - Has ongoing cost if not attached to EC2 instance, or if the EC2 instance is stopped.

- Internet Protocol version 6 (IPv6)
  - Every IP address is public.

### VPC, Subnet, Internet Gateway, NAT Gateways

#### Virtual Private Cloud (VPC)

- Private network to deploy your resources
- A VPC is linked to a specific region
  - Need multiple VPC if we are working in multiple AWS regions.

#### Subnet

- Allow you to partition your network inside your VPC
- AZ-specific resource
- A public subnet is a subnet that is accessible from the internet.
- A Private subnet is a subnet that is not accessible from the internet.
- To define access to the internet and between subnets, we use Route Tables.

#### Internet Gateway

- Helps our VPC instances connect with the internet
- Public subnets have a route to the internet gateway.
- NAT Gateways (AWS-managed) & NAT Instances allow your instances in your Private subnets to access the internet while remaining private.

### Security Groups and Network Access Control List (NACL)

- NACL
  - First line of defense for EC2 instance.
  - Firewall which controls traffic to and from the subnet.
  - Are attached at the Subnet level
  - Supports _ALLOW_ and _DENY_ rules.
  - Rules only include IP addresses.

- Security Groups
  - A firewall that controls traffic to and from an EC2 instance.
  - Can have only _ALLOW_ rules.
  - Rules include IP addresses and other security groups.

### VPC Flow Logs

- Capture information about IP traffic going into your interfaces
- Helps to monitor and troubleshoot connectivity issues
  - Subnets to internet
  - Internet to subnets
  - Subnets to subnets
- Captures network information from AWS managed interfaces
  - Elastic Load Balancers
  - ElastiCache
  - RDS
  - Aurora
- VPC Flow logs data can go to S3, CloudWatch Logs, and Kinesis Data Firehose

### VPC Peering

- Connect two VPC privately using AWS' network.
- Make them behave as in they were in the same network.
- Must not have overlapping CIDR (IP address range)
- VPC Peering connection is not transitive.
  - If VPC1 -> VPC2, and VPC2 -> VPC3, this does not imply VPC1 -> VPC3.
  - Must be established for each VPC that need to communicate with one another.

### VPC Endpoints

- Endpoints allow you to connect to AWS Services using a private network in of the public `www` network
- This gives you enhanced security and lower latency to access AWS services
- VPC Endpoint Gateway: S3 & DynamoDB
- VPC Endpoint Interface: Other AWS services

#### AWS PrivateLink

- Most secure & scalable way to expose a service to 1000s of VPCs
- Does not require VPC peering, internet gateway, NAT, route tables
- Requires a network load balancer and Elastic Network Interface (ENI)
  - Establish private link between network load balancer, and ENI
  - All internet traffic will then go through this private network.
  - All people need to do is to create more private links

### Direct Connect & Site-to-Site VPN

#### Site to Site VPN

- Connect an on-premises VPN to AWS
  - Must use a Customer Gateway (CGW) on the on-premise site.
  - Must use a Virtual Private Gateway (VGW) on the AWS site.
- Connection is automatically encrypted
- Goes over the public internet
  - Limited bandwidth
  - Security Concerns
- Takes just a few minutes to establish.

#### Direct Connect

- Establish a physical connection between on-premises and AWS
- The connection is private, secure and fast
- Goes over the private network
  - More secure
  - Faster
- Takes at least a month to establish

### Client VPN

- Connect from your computer using OpenVPN to your private network in AWS and on-premises.
- Allow you to connect to your EC2 instances over a private IP
  - Just as if you were in the private VPC network
- Goes over public Internet

### Transit Gateway

- For having transitive peering between thousands of VPC and on-premises, star connection
- One single Gateway to provide this functionality
- Works with Direct Connect Gateway, VPN connections

## Security & Compliance

### AWS Shared Responsibility Model

- AWS Responsibility
  - Protecting infrastructure that runs all the AWS services
  - Managed services
- Customer Responsibility
  - For management of the guest OS
  - Configuring firewall & network configuration
  - IAM
  - Encrypting application data according to compliance requirements
- Shared controls
  - Patch Management
  - Configuration Management
  - Awareness & Training

### DDoS Protection: WAF & Shield

- Distributed Denial-of-Service (DDoS) Attack
  - Attacker overwhelms the server with a lot of requests.
  - Users will find server inaccessible and unresponsive.
- Be ready to scale by using ASG on AWS in event of a DDoS attack.
- AWS Shield Standard
  - Free service that is activated for every AWS customer.
  - Protects against DDoS attack for website at no additional costs
- AWS Shield Advanced.
  - Optional DDoS mitigation service
    - $3000 per month per organization.
  - Protect against more sophisticated attacks on AWS services.
  - Protect against higher fees during usage spikes due to DDoS.
  - 24/7 premium DDoS protection.
- AWS WAF
  - Protects your web applications from common web exploits on Layer 7
    - Layer 7 is HTTP
    - Deploy on ALB, API Gateway, CloudFront
  - Define Web Access Control List
    - Rules can include IP addresses, HTTP headers, HTTP body, or URI strings
    - Protects from common attacks
    - Size constraints, geo-match
    - Rate-based rules for DDoS protection
  - Filter specific requests based on rules.
- CloudFront and Route53
  - Availability protection using global edge network.
  - Combined with AWS Shield, provides attack mitigation at the edge.

### Penetration Testing

- AWS customers are welcome to carry out security assessments or penetration tests against their AWS infrastructure without prior approval for these services:
  1. Amazon EC2 instances, NAT Gateways, ELBs
  2. Amazon RDS
  3. Amazon CloudFront
  4. Amazon Aurora
  5. Amazon API Gateways
  6. AWS Lambda and Lambda Edge functions
  7. Amazon Lightsail resources
  8. Amazon Elastic Beanstalk environments
- Prohibited Activities
  - DNS zone walking via Amazon Route 53 Hosted Zones
  - Simulated Denial-of-Service, Simulated Distributed Denial-of-Service
  - Port flooding
  - Protocol flooding
  - Request flooding

### Encryption with KMS & CloudHSM

### Protecting Data

- Leverage on Encryption keys to protect two types of data

1. Data at rest
    - Data stored or archived on a device
    - Not moving because it is stored somewhere.
2. Data in transit
    - Data being moved from one location to another
    - Transfer from on-premises to AWS, EC2 to DynamoDB, etc.

### AWS Key Management Service (KMS)

- AWS manages the encryption keys for us
- Encryption Opt-in
  - EBS Volumes: Encrypt volumes
  - S3 buckets: Server-side encryption of objects
  - Redshift database: Encryption of data
  - RDS database: Encryption of data
  - EFS drives: Encryption of data
- Encryption automatically enabled for:
  - CloudTrail Logs
  - S3 Glacier
  - Storage Gateway

### CloudHSM

- AWS provisions encryption hardware, but we are managing the encryption ourselves.
  - Dedicated Hardware
  - Hardware Security Module (HSM) device is tamper resistant

#### Types of Customer Master Keys (CMK)

- Customer Managed CMK
  - Create, manage and used by the customer, can enable or disable
  - Possibility of rotation policy
    - New key generated every year, old key preserved
  - Possibility to bring-your-own-key
- AWS managed CMK
  - Created, managed and used on the customer’s behalf by AWS
  - Used by AWS services
    - AWS S3
    - AWS EBS
    - AWS Redshift
- AWS owned CMK
  - Collection of CMKs that an AWS service owns and manages to use in multiple accounts
  - AWS can use those to protect resources in your account
    - You cannot view the keys
- CloudHSM Keys (Custom keystore)
  - Keys generated from your own CloudHSM hardware device
  - Cryptographic operations are performed within the CloudHSM cluster

### AWS Certificate Manager (ACM)

- Allows user to easily provision, manage, and deploy SSL/TLS Certificates
  - Used to provide in-flight encryption for website (HTTP)
- Supports both public and private TLS certificates
- Free of charge for public TLS certificates
- Automatic TLS certificate renewal
- Integrations with
  - Elastic Load Balancers
  - CloudFront Distributions
  - APIs on API Gateway
  - Integration done by loading TLS certificates on the services

### AWS Secrets Manager

- Newer service, meant for storing secrets.
  - Paid Service, 40-cents per secret per month.
- Capability to force rotation of secrets every few days.
- Automate generation of secrets on rotation using Lambda.
- Integration with Amazon RDS.
  - Secrets Manager is used to create passwords for Amazon RDS automatically.
  - Mostly meant for RDS integration.
- Secrets are encrypted using KMS.

### AWS Artifact

- Not really a service, but is presented as one in the console.
- A portal that provides access on-demand to AWS compliance documentation and AWS agreements.
- Displays Artifact Reports
  - Allows you to download AWS security and compliance documents from third-party auditors.
- Displays Artifact Agreements
  - Allows you to review, accept, and track the status of AWS agreements for an individual account, or in your organization.
- Can be used to support internal audit or compliance.

### AWS GuardDuty

- Intelligent Threat discovery to protect your AWS Account
- Uses Machine Learning algorithms
  - Performs anomaly detection on 3rd party data to detect threats.
  - Input data for Amazon Guard Duty:
    1. VPC Flow Logs
    2. CloudTrail Logs
    3. AWS DNS Logs
    4. EKS Audit Logs
- Can setup EventBridge rules to be notified in case of findings.
  - EventBridge rules can target AWS Lambda or SNS.
- Can protect against CryptoCurrency attacks.
- One click to enable, with no need to install the software.

### AWS Inspector

- Automated Security Assessments only on:
  - EC2 instances
    - Leveraging the AWS SSM agent
    - Analyze against unintended network accessibility.
    - Analyze the running OS against known vulnerabilities.
  - Container Image pushes to Amazon ECR
    - Assessment of Container Images as they are pushed.
  - Lambda Functions
    - Identifies software vulnerabilities in function code and package dependencies.
    - Assessment of functions as they are deployed.
- Continuous scanning of the infrastructure, only when needed.
- A risk score is associated with all vulnerabilities for prioritization.
- Can report its findings into the AWS Security Hub.
- Sends findings to Amazon EventBridge.
  - Can use AWS Lambda or SNS for automation.

### AWS Config

- Per-region service that is payable
  - Can be aggregated across regions and accounts.
- Helps with auditing and recording compliance of your AWS resources.
  - View compliance of a resource over time
  - View CloudTrail API calls if enabled.
  - Apply configuration rules on the AWS resources in the account.
- Helps record configurations and changes over time.
  - View configuration of a resource over time
- Possibility of storing the configuration data into S3
- Receive alerts on SNS notifications for any changes done to the infrastructure.

### AWS Macie

- Fully managed data security and data privacy service
  - Uses ML and pattern matching to discover and protect your sensitive data in AWS
  - Helps identify and alert you to sensitive data, such as personally identifiable information (PII).
- Macie will discover sensitive data in your S3 bucket, and notify you via Amazon EventBridge.

### AWS Security Hub

- Central security tool to manage security across several AWS accounts, and automate security checks.
- Integrated dashboards showing current security and compliance status to quickly take actions.
  - Makes it way simpler for users to find security issues and remediate them.
- Automatically aggregates alerts in pre-defined or personal finding formats from various AWS services and AWS partner tools.
  - Collect potential issues and findings, and then generate events via EventBridge.
- Must first enable AWS Config Service.

### Amazon Detective

- GuardDuty, Macie and Security Hub are used to identify potential security issues or findings.
- Detective analyzes, investigates, and quickly identify the _root cause_ of security issues or suspicious activities
  - Using ML and graphs
  - Automatically collects and processes events from VPC Flow Logs, CloudTrail, GuardDuty, and create a unified view.
  - Produces visualizations with details and context to get to the root cause.

### AWS Abuse

- Report suspected AWS resources used for abusive illegal purposes.
  - Spams
  - Port scanning
  - DoS or DDoS attacks
  - Intrusion attempts
  - Hosting objectionable or copyrighted content
  - Distributing malware
- Contact the AWS Abuse team via an online abuse form, or to _abuse@amazonaws.com_

### Root User Privileges

- Root user has complete access to _all_ AWS services and resources.
  - Lock away your AWS account root user access keys.
- Do not use the root account for everyday tasks, even administrative tasks.
- Only the _root user_ can
  - Change account settings
  - View certain tax invoices
  - Close your AWS account
  - Restore IAM user permissions
  - Change or cancel your AWS Support plan
  - Register as a seller in the Reserved Instance Marketplace
  - Configure an Amazon S3 bucket to enable MFA
  - Edit or delete an Amazon S3 bucket policy that includes an invalid VPC ID or VPC endpoint ID
  - Sign up for GovCloud

### IAM Access Analyzer

- Find out which resources are shared externally.
- Define Zone of Trust
  - Anything outside the Zone of Trust that have access to the AWS resources, are going to be reported as findings.
  - Findings are then put onto the console, where the user can then decide to take action against these findings.

## Machine Learning

### Amazon Rekognition

- Find objects, people, text, scenes in images and videos using Machine Learning.
- Facial analysis and facial search to do user verification, people-counting, etc.
- Use Cases:
  - Labeling
  - Content Moderation
  - Text Detection
  - Face Detection and Analysis
  - Face Search and Verification
  - Celebrity Recognition
  - Pathing
    - For Sports games analysis

### Amazon Transcribe

- Automatically convert speech to text
- Uses a deep learning process called automatic speech recognition (ASR) to convert speech to text quickly and accurately.
- Automatically remove PII using Redaction
- Supports Automatic Language Identification for multi-lingual audio
- Use Cases:
  - Transcribe customer service calls.
  - Automate closed captioning and subtitling
  - Generate metadata for media assets to create a fully searchable archive.

### Amazon Polly

- Turn text into speech using deep learning
- Create applications that talk.

### Amazon Translate

- Natural and accurate language translation
- Localize content for international users, and to easily translate large volumes of text efficiently.

### Amazon Lex & Connect

#### Amazon Lex

- Automatic Speech Recognition (ASR) to convert speech to text
- Natural Language Understanding to recognize the intent of text, callers
- Useful for building chat-bots, and call center bots.

#### Amazon Connect

- Receive calls, create contact flows, cloud-based virtual contact center
- Can integrate with other CRM systems or AWS
- No upfront payments, 80% cheaper than traditional contact center solutions.

### Amazon Comprehend

- For Natural Language Processing
- Fully managed and serverless service
- Uses machine learning to find insights and relationships in text
  - Language of the text
  - Extracts key phrases, places, people, brands or events
  - Understands how positive or negative the text is
  - Analyzes text using tokenization and parts of speech
  - Automatically organizes a collection of text files by topic
- Use Cases:
  - Create and group articles by topics
  - Analyze customer interactions to find what leads to a positive or negative experience

### Amazon SageMaker

- Fully managed service for developers / data scientists to build Machine Learning models

### Amazon Forecast

- Fully managed service that uses Machine Learning to deliver highly accurate forecasts
- Can use data stored in Amazon S3 to train the model.
- Use Cases:
  - Product Demand Planning
  - Financial Planning
  - Resource Planning

### Amazon Kendra

- Fully managed document search service powered by Machine Learning
- Extract answers from within a document
  - Natural language search capabilities
  - Learn from user interactions / feedback to promote preferred results
  - Ability to manually fine-tune search results.

### Amazon Personalize

- Fully managed Machine Learning service to build applications with real-time personalized recommendations.
- Use Cases:
  - Retail stores
  - Media and entertainment

### Amazon Textract

- Automatically extracts text, handwriting, and data from any scanned documents using AI and ML.
- Extract data from forms and tables.
- Read and process any type of document
  - PDF
  - Images
- Use Cases:
  - Financial Services
  - Healthcare
  - Public Sector

## Advanced Identity

### AWS Security Token Service (STS)

- Enables you to create temporary, limited privileges credentials to access your AWS resources.
- Short-term credentials
  - Configurable expiration period.
- Use Cases:
  - Identity federation
  - IAM Roles for cross/same account access
  - IAM Roles for Amazon EC2

### Amazon Cognito

- Identity for your Web and Mobile applications users
- Instead of creating IAM user accounts for these users, we can create a user in Cognito

### Directory Services

- Integrates Microsoft Active Directories into AWS

### AWS IAM Identity Center

- _One login_ for _all_ your AWS accounts in AWS Organizations
- Identity providers
  - Built-in identity store in IAM Identity Center
  - 3rd Party:
    - Microsoft Active Directory
    - OneLogin
    - Okta
