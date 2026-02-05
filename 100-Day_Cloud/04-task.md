## Task
Data protection and recovery are fundamental aspects of data management.
It's essential to have systems in place to ensure that data can be recovered in case of accidental deletion or corruption.
The DevOps team has received a requirement for implementing such measures for one of the S3 buckets they are managing.

The s3 bucket name is datacenter-s3-9256, enable versioning for this bucket.

## Solutions

******
### List the s3 bucket
```
aws s3api put-bucket-versioning --bucket amzn-s3-demo-bucket1 --versioning-configuration Status=Enabled

```

### Apply the version control

```
aws s3api put-bucket-versioning --bucket datacenter-s3-9256 --versioning-configuration Status=Enabled

```
			
