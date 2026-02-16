## Task

The Nautilus DevOps team has been creating a couple of services on AWS cloud. 
They have been breaking down the migration into smaller tasks, allowing for better control, risk mitigation, 
and optimization of resources throughout the migration process. Recently they came up with requirements mentioned below.

There is an instance named xfusion-ec2 and an elastic-ip named xfusion-ec2-eip in us-east-1 region. 
Attach the xfusion-ec2-eip elastic-ip to the xfusion-ec2 instance.

## Solutions

- Get the instance ID

```
INSTANCE_ID=$(aws ec2 describe-instances \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=xfusion-ec2" \
  --query "Reservations[].Instances[].InstanceId" \
  --output text)
  ```
- Get The Allocation ID

```
ALLOCATION_ID=$(aws ec2 describe-addresses \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=xfusion-ec2-eip" \
  --query "Addresses[].AllocationId" \
  --output text)

  ```

- Attache Elastic IP

```
aws ec2 associate-address \
  --region us-east-1 \
  --instance-id $INSTANCE_ID \
  --allocation-id $ALLOCATION_ID

```

  
