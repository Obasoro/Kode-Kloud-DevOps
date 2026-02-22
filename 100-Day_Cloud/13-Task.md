## Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. 
Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive 
transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team 
to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. 
By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, 
allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, create an AMI from an existing EC2 instance named nautilus-ec2 with the following requirement:

Name of the AMI should be nautilus-ec2-ami, make sure AMI is in available state.

## Solutions

- Get the Instance ID

```sh

INSTANCE_ID=$(aws ec2 describe-instances \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=nautilus-ec2" \
  --query "Reservations[].Instances[].InstanceId" \
  --output text)
```

- Create the AMI

```sh

AMI_ID=$(aws ec2 create-image \
  --region us-east-1 \
  --instance-id $INSTANCE_ID \
  --name "nautilus-ec2-ami" \
  --description "AMI for nautilus-ec2 instance" \
  --query "ImageId" \
  --output text)

echo "AMI Creation started. AMI ID: $AMI_ID"

```

- Wait for "Available" State

```
echo "Waiting for AMI to become available..."
aws ec2 wait image-available \
  --region us-east-1 \
  --image-ids $AMI_ID

echo "Success! AMI $AMI_ID is now in an available state."

```
