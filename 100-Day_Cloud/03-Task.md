## Task
****
The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. 
Recognizing the scale of this undertaking, they have opted to approach the 
migration in incremental steps rather than as a single massive transition.

For this task, create one subnet named xfusion-subnet under default VPC.

****

## Solution

- List available default [VPC-ID]
- List the various cidr-block subnet taken
- create VPC


```
aws ec2 describe-vpcs --filters "Name=isDefault,Values=true" --query "Vpcs[0].VpcId" --output text

```
aws ec2 describe-vpcs --filters "Name=isDefault,Values=true" --query "Vpcs[0].CidrBlock" --output text

```

```
aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-06ee8fa736ec74fad"
--query "Subnets[*].[SubnetId,CidrBlock,AvailabilityZone]" --output table

```
```
# Option 1: Use /20 (4096 addresses)
aws ec2 create-subnet \
    --vpc-id vpc-06ee8fa736ec74fad \
    --cidr-block 172.31.48.0/20 \
    --availability-zone us-east-1a \
    --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=xfusion-subnet}]'
```
