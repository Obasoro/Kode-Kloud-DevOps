## Task

The Nautilus DevOps team has been creating a couple of services on AWS cloud. They have been breaking down the migration into smaller tasks, 
allowing for better control, risk mitigation, and optimization of resources throughout the migration process. 
Recently, they came up with requirements mentioned below.

An instance named devops-ec2 and a volume named devops-volume already exist in uthe s-east-1 region. 
Attach the devops-volume volume to the devops-ec2 instance, make sure to set the device name to /dev/sdb while attaching the volume.

## Solution

- # 1. Get the Instance ID
```sh
INSTANCE_ID=$(aws ec2 describe-instances \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=devops-ec2" "Name=instance-state-name,Values=running,stopped" \
  --query "Reservations[].Instances[0].InstanceId" \
  --output text)

```

- # 2. Get the Volume ID

```
VOLUME_ID=$(aws ec2 describe-volumes \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=devops-volume" \
  --query "Volumes[0].VolumeId" \
  --output text)

```

- # 3. Attach the Volume

```
aws ec2 attach-volume \
  --region us-east-1 \
  --volume-id $VOLUME_ID \
  --instance-id $INSTANCE_ID \
  --device /dev/sdb

```
