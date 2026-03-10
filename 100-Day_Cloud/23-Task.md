## Task

As part of a data migration project, the team lead has tasked the team with migrating data from an existing S3 bucket to a new S3 bucket. The existing bucket contains a substantial amount of data that must be accurately transferred to the new bucket. The team is responsible for creating the new S3 bucket and ensuring that all data from the existing bucket is copied or synced to the new bucket completely and accurately. It is imperative to perform thorough verification steps to confirm that all data has been successfully transferred to the new bucket without any loss or corruption.

As a member of the Nautilus DevOps Team, your task is to perform the following:

Create a New Private S3 Bucket: Name the bucket nautilus-sync-31818.

Data Migration: Migrate the entire data from the existing nautilus-s3-22123 bucket to the new nautilus-sync-31818 bucket.

Ensure Data Consistency: Ensure that both buckets have the same data.

## Solutions

- Create the new private S3 bucket

```
aws s3api create-bucket \
  --bucket nautilus-sync-31818 \
  --region us-east-1

# Block all public access (make it private)
aws s3api put-public-access-block \
  --bucket nautilus-sync-31818 \
  --public-access-block-configuration \
  "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"

```

- Migrate all data from the source bucket

```
aws s3 sync s3://nautilus-s3-22123 s3://nautilus-sync-31818

```

- Verify the migration

```
# Count objects in source
aws s3 ls s3://nautilus-s3-22123 --recursive --summarize | tail -2

# Count objects in destination
aws s3 ls s3://nautilus-sync-31818 --recursive --summarize | tail -2

```
