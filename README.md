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
  - High frequency online transaction processing systems (OLTP)
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
- Security groups are locked down to a region/VPC combination
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


| AWS                                      | User                                   |
| ---------------------------------------- | -------------------------------------- |
| Infrastructure                           | S3 Versioning                          |
| Configuration and Vulnerability Analysis | S3 Bucket Policies                     |
| Compliance Validation                    | S3 Replication Setup                   |
|                                          | Logging and Monitoring                 |
|                                          | S3 Storage Classes                     |
|                                          | Data encryption at rest and in transit |
