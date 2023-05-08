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
1. Free Tiers
- t2.micro (Free for up to 750h/month)

2. Paid Tiers
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
- Most general purpose instance types have the `T, M, A` name

#### Compute Optimized Instance Types
- Great for Compute-intensive tasks that require high performance processors:
    - Batch processing workloads
    - Media transcoding
    - High performance web servers
    - High performance computing
    - Scientific modeling & machine learning
    - Dedicated gaming servers
- Most compute optimized instance types have the `C` name

#### Memory Optimized Instance Types
- Fast performance for workloads that process large data sets in memory:
    - High performance, relational/non-relational databases
    - Distributed web scale cache stores
    - In-memory databases optimized for Business Intelligence
    - Applications performing real-time processing of big unstructured data
- Most memory optimized instance types have the `R, X, z` name

#### Storage Optimized Instance Types
- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage:
    - High frequency online transaction processing systems (OLTP)
    - Relational & NoSQL databases
    - Cache for in-memory databases
    - Data warehousing applications
    - Distributed file systems
- Most storage optimized instance types have the `I, D, H` name

### Security Groups
#### Introduction to Security Groups
- Security Groups are the fundamental of network security in AWS
- They control how traffic is allowed into or out of our EC2 instance
- Security groups only contain *allow* rules
- Security groups rules can reference by IP or by security group
- Security groups can be attached to multiple instances

#### Security Groups as a firewall
- Security groups are acting as a firewall on EC2 instances.
- They regulate
    1. Access to Ports
    2. Authorised IP ranges - IPv4, IPv6
    3. Control of inbound network
    4. Control of outbound network
- All inbound traffic is blocked by default
- All outbound traffic is authorised by default
- Security groups are locked down to a region/VPC combination
- Lives *outside* the EC2 instance
    - If traffic is blocked, the EC2 instance cannot see the inbound network
- Common errors for EC2 instances:
    - Application timeout: Security group issue
    - Connection refused error: Application error / Application is not launched
- It is good to maintain one seperate security group for SSH access

### Classic ports to know
- FTP (File Transfer Protocol): *21*
    - Upload files into a file share
- SFTP (Secure File Transfer Protocol): *22*
    - Upload files using SSH
- SSH (Secure Shell): *22*
    - Logs into a Linux Instance
- HTTP: *80*
    - Access unsecured websites
- HTTPS: *443*
    - Access secured websites
- RDP (Remote Desktop Protocol): *3389*
    - Log into a Windows Instance

### SSH
#### Connectivity Summary Table

EC2 Instance Connect uses the web browser to connect to EC2 Instance, and only works with Amazon Linux 2.

|            |SSH |PuTTY|EC2 Instance Connect|
|------------|----|-----|--------------------|
|Mac         |X   |     |X                   |
|Linux       |X   |     |X                   |
|Windows <10 |    |X    |X                   |
|Windows >=10|X   |X    |X                   |

#### SSH using Linux or Mac or Windows >= 10
- SSH using .pem Key Pair: Navigate to the directory containing the .pem file, and enter:

    `ssh -i <File Name> ec2-user@<Public IP>`
<br></br>

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
|AWS                            |User                                                  |
|-------------------------------|------------------------------------------------------|
|Infrastructure                 |Security Groups rules                                 |
|Isolation on physical hosts    |OS patches and updates                                |
|Replacing faulty hardware      |Software and utilities installed on the EC2 instance  |
|Compliance validation          |IAM Roles assigned to EC2 & IAM user access management|
|                               |Data security on your instance                        |

## EC2 Instance Storage
### Elastic Block Store Volume
- A network drive you can attach to your instances while they run
    - Uses the network to communicate the instance, thus meaning that there might be a bit of latency
    - Can be detached from an EC2 instance, and attached to another one quickly
    - We can also leave them unattached on creation, and attach them on-demand
- Allows your instances to persist data, even after their termination
- Can only be mounted to *one instance at a time*
    - EBS Volume types *io1, io2* are exceptions to this rule, with them providing a EBS Multi-Attach feature.
- Bound to a specific AZ (Availability Zone)
    - An EBS Volume in *us-east-1a* cannot be attached to an EC2 instance in *us-east-1b*
    - To move a volume across, you first need to snapshot it
- Free tier provides 30GB of free EBS storage of type SSD, or Magnetic Disk, per month
    - Has a provisioned capacity, meaning that we specify how much storage we want beforehand

#### EBS Delete on Termination Attribute
- Controls the EBS behaviour when an EC2 instance terminates
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
    - Move a Snapshot to an *archive tier*, that is 75% cheaper.
    - Takes within *24 to 72 hours* for restoring the archive

- Recycle Bin for EBS Snapshots
    - Setup rules to retain deleted snapshots so you can recover them after an accidental deletion
    - Retention period can be specified
        - From 1 day to 1 year

