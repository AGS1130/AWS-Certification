# AWS-Certification
Study Guide for Developer and Solutions Architect Certificates 

### AWS FAQ (Read The Night Before the Exam)

  * [EC2](https://aws.amazon.com/ec2/faqs/)
  * [VPC](https://aws.amazon.com/vpc/faqs/)
  * [Lambda](https://aws.amazon.com/lambda/faqs/)
  * [S3](https://aws.amazon.com/s3/faqs/)
  * [RDS](https://aws.amazon.com/rds/faqs/)
  * [DynamoDB](https://aws.amazon.com/dynamodb/faqs/)
  * [Route53](https://aws.amazon.com/route53/faqs/)
  
## S3 (Simple Storage Service)

### S3 Object Storage Classes
  * S3-Standard - Durability of 99.999999999% and availability of 99.99%.

  * S3-IA (Infrequently Accessed) - Durability of 99.999999999% and availability of 99.9%.

  * S3-RRS (Reduced Redundancy Storage) - Durability and availability of 99.99%. Use when you don’t care if data is occasionally lost and can easily be re-created.

  * Glacier - For archival only. Takes 3 - 5 hours to restore files. Durability of 99.999999999%.

  * S3 Buckets
### S3 Namespace is global. Region independent.

  * A bucket name in any region should only contain lower case characters. It has to be DNS Compliant

  * Object versioning - Different versions of the same object in a bucket.

  * Only Static website can be hosted. Auto scaling, Load Balancing etc. all managed automatically.

  * You can tag buckets (or any AWS resoruce) to track costs. Tags consist of keys and (optional) value pairs.

  * Lifecycle management of objects can be set. e.g. move to Glacier after 30 days

  * Every bucket created, object uploaded is private by default.

  * Object Permissions – Access to Object ACLs

  * Prefix in bucket is a folder in the bucket.

  * Minimum file size that I can store on S3 bucket is 0 byte.

  * Max 100 S3 buckets per account by default.

  * Individual Amazon S3 objects can range in size from a minimum of 0 bytes to a maximum of 5 terabytes. The largest object that can be uploaded in a single PUT is 5 gigabytes. For objects larger than 100 megabytes, customers should consider using the Multipart Upload capability.

### S3 Versioning
  * Once versioning is turned on it cannot be removed. It can only be suspended. To remove versioning, you have to create a new bucket and transfer all files from old to new

  * For newer version of an object, you still have to set permissions to allow access. It is disabled by default even if previous version is public.

  * All versions of the file add up to the storage. Hence for larger objects, ensure that there is some lifecycle versioning in place.

  * Version deleted cannot be restored.

  * Object deleted can be restored – Delete the Delete marker.

  * Versioning is a good backup tool.

  * For versioning. MFA can be setup for Delete capability for object / bucket – Complicated setup.
  
### S3 Versioning Exam Tips:

  * Stores all versions of the object(all writes and deletes)
  
  * Great backup tool
  
  * Once enabled, versioning cannot be disabled, only suspended
  
  * Integrates with lifecycle rules
  
  * Versioning's MFA delete capability, which uses multi-factor authentication, can be used to provide additional security
    cross region replication requires versioning enabled on the source bucket
    

### S3 Lifecycle management:

  * Can be used in conjunction with versioning

  * Can be applied to current versions and previous versions.

  * Following actions are allowed in conjunction with or without versioning:

    * archive to Glacier storage class(30 days after IA, if relevant)

    * permanent delete

    * archive and permanent delete
   
    * transition to the Standard: Infrequent Access Storage class(128kb and 30 days after the creation date)

### S3 Lifecycle management Exam tips:

  * Can be used with versioning
  * Can be applied to current and previous versions
  * Following actions can now be done
      * Transition to Standard-IA(128kb and 30 days after creation date)
      * Archive to glacier storage class(30 days after IA)
      * permanently delete

### S3 Security:

   * All buckets are PRIVATE by default. That means, if you were to type in the buckets publicly accessible URL address, and it’s not a publicly available bucket, you wouldn’t be able to access object within that bucket. You would have actually go in and make that bucket public
   * Allows Access Control Lists (an individual user can only have access to 1 bucket and have read only access)
   * Integrates with IAM using roles,for example allows EC2 users to have access to S3 buckets by roles
   * All endpoints are encrypted by SSL
   * S3 buckets can be configured to create access logs which log all the requests made to the S3 bucket. This can be done to another bucket

### S3 Functionality:

  * Static websites can be hosted on S3. No need for webservers, you can just upload a static .html file to an S3 bucket and take advantage of AWS S3’s durability and High Availability
  
  * Integrates with Cloud Front CDN,which is Amazon’s own Content Delivery Network
  
  * Multipart uploads, allows you to upload parts of a file concurrently
  
  * Suggested for files over 100MB.It is required for any files over 5GB
  
  * Allows us to resume a stopped file upload
  
  * S3 is spread across multiple availability zones, and they guarantee Eventual consistency. All AZ’s will eventually be consistent.    Put/Write/Delete requests will eventually be consistent across AZ’s

### S3 use Cases:

  * File shares for networks
  
  * Backup/archiving
  
  * Used as an origin for CloudFront’s Content Distribution Network
  
  * Hosting static files
  
  * Hosting static websites

## VPC (Virtual Private Cloud)

### Introduction
  * VPC is a logical data center within an AWS Region.

  * Control over network environment, select IP address range, subnets and configure route tables and gateways.

  * Do not span regions, but can span AZs.

  * Can create public facing subnet (Web) having internet access and private facing subnet (DB) with no internet access

  * Public Subnet – Web Servers/ Jump Boxes

  * Private Subnet – Applications Servers / Database servers

  * Leverage multiple layers of security – Security groups and Network ACLs to control access to EC2 instances

  * Create hardware VPN connection between your local DC and AWS.

  * AWS gives a maximum of /16 network.

  * Bastion host/ Jump Box in Public subnet

  * Security groups, Network ACLs, Route Tables can span subnets/AZs.

  * Each subnet is always mapped to an availability zone. 1 subnet = 1 AZ

  * Only one internet gateway per VPC. [Trick question – improve performance by adding Gateway – just not possible]

  * Security groups are stateful. Network ACLs are stateless.

  * By default, how many VPCs am I allowed in each AWS Region? == 5

  * Typical Private IP address ranges – not publically routable.

  * 10.0.0.0 - 10.255.255.255 (10/8 prefix)

  * 172.16.0.0 - 172.31.255.255 (172.16/12 prefix)

  * 192.168.0.0 - 192.168.255.255 (192.168/16 prefix)

  * Virtual data centre in the cloud
  
  * A logically isolated section of AWS cloud where you can launch AWS resources in a virtual network you define
  
  * You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, network access control lists, configuring route tables, and network gateways
  
  * 1 subnet = 1 AZ
  
  * Security groups are stateful, network access control lists are stateless, i.e. with nacls we will need to open both inbound and outbound ports for eg for port 80, but not with security groups
  
  * Subnets and ACLs provide much better security over your AWS resources
  
  * Instances security groups, they span multiple AZs and hence can span multiple VPCs
  
  * Subnet acls
  
  * Default vs custom vpc
  
    * Default allows you to deploy immediately, user friendly
    
    * All subnets have a route to the internet, do not get private subnets in default vpc
    
    * Each ec2 instance will has private and public IP address, in a custom vpc with a private subnet we won't get a public ip address we only get a private address
    
   * VPC peering
   
      * Allows you to connect 1 vpc to another via direct connect route using private ip
      
      * Instances behave as if they were on the same private network
      
      * Peering possible with vpcs in the same aws account or in different aws accounts
      
      * Always a star configuration, 1 central VPC peers with 4 others. No transitive peering!
      
  * Whenever you create a new VPC AWS creates a default ACL, a default security group, and a route, but it won't create a subnet, you will need to create one yourself
  
  * Always going to loose 5 ip addresses when you create a subnet, since those 5 are reserved by Amazon
  
  * You can have 1 NAT gateway for 1 custom vpc
  
  * Allowed to have 5 VPCs in a region

### Default v/s Custom VPC
  * When you create an account a default VPC is created for you in each Region.

  * All subnets in default VPC have a route out to the internet

  * Each EC2 instance in default VPC will have a public and private IP address

  * If you delete default VPC, only way to restore it is by contacting Amazon.

### Custom VPC Info
  * Default Security group, network ACL & route table are created for each custom VPC you create.

  * Doesn’t create subnets or internet gateways out of the box.

  * In each VPC you create, 5 IP addresses are reserved by AWS for itself. First 4 and last IP in the CIDR block.

  * You can't change the size of a VPC after you create it. If your VPC is too small to meet your needs, create a new, larger VPC, and then migrate your instances to the new VPC. To do this, create AMIs from your running instances, and then launch replacement instances in your new, larger VPC. You can then terminate your old instances, and delete your smaller VPC. 

  * You can’t attached multiple Internet Gateways to the VPC to boost performance.

  * When creating VPCs do not modify default route table to add your custom rules. If you modify the default route, it will affect all instances. Create a new route table for customization.

### NAT Instance & NAT Gateway

  * NAT Instance is one EC2 instance. You are responsible for performance management, scale out and security groups. NAT Gateway is a managed service.

  * On NAT instance, remember to disable source/destination IP check. This is required to allow private subnet internet connectivity. This is not required on NAT Gateway.

  * Allow both HTTP and HTTPS access on security groups associated with NAT instances. Security groups are always associated with NAT Instances.

  * Both NAT Instance and NAT Gateways are deployed to public subnet. Elastic IP has to be added to NAT Instance. NAT Gateway is automatically assigned a public IP.

  * In VPC, update default route table to allow connectivity from Private subnet to NAT Instance and Gateway

  * NAT instance is single point of failure. You can place NAT instance behind Auto Scaling group, multiple subnets in different AZs and scripted failover. To improve performance increase the size of the NAT instance to allow for higher throughput.

  * You can use Network ACLs to control traffic for both NAT Instance and Gateway.

  * NAT Gateways scale up to 10GBps. No need to disable source/ destination checks on Gateways.

### Create Links

### EC2
