## Task

The Nautilus DevOps team has been creating a couple of services on AWS cloud. They have been breaking down the migration 
into smaller tasks, allowing for better control, risk mitigation, and optimization of resources throughout the migration 
process. Recently they came up with requirements mentioned below.

An instance named datacenter-ec2 and an elastic network interface named datacenter-eni already exists in us-east-1 region.

Attach the datacenter-eni network interface to the datacenter-ec2 instance.
Make sure status is attached before submitting the task.

## Solutions

# Get Instance ID
```INSTANCE_ID=$(aws ec2 describe-instances \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=datacenter-ec2" \
  --query "Reservations[].Instances[].InstanceId" \
  --output text)

```

# Get ENI ID
```
ENI_ID=$(aws ec2 describe-network-interfaces \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=datacenter-eni" \
  --query "NetworkInterfaces[].NetworkInterfaceId" \
  --output text)

```

# Attach Elastic Ip to datacenter

```
aws ec2 attach-network-interface \
  --region us-east-1 \
  --instance-id $INSTANCE_ID \
  --network-interface-id $ENI_ID \
  --device-index 1

  ```

### Verify connection

```bash
echo "Waiting for ENI to be attached..."
while true; do
    STATUS=$(aws ec2 describe-network-interfaces \
      --region us-east-1 \
      --network-interface-ids $ENI_ID \
      --query "NetworkInterfaces[0].Attachment.Status" \
      --output text)

    if [ "$STATUS" == "attached" ]; then
        echo "Status: $STATUS"
        break
    else
        echo "Current status: $STATUS... retrying in 5 seconds"
        sleep 5
    fi
done

```
