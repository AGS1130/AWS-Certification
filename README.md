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

# VPC (Virtual Private Cloud)

## To be done
