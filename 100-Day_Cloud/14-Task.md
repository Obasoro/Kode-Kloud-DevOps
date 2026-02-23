## Task

During the migration process, several resources were created under the AWS account. Later on, some of these resources became 
obsolete as alternative solutions were implemented. Similarly, there is an instance that needs to be deleted as it is no longer in use.

1) Delete the ec2 instance named devops-ec2 present in us-east-1 region.

2) Before submitting your task, make sure instance is in terminated state.

## Solution

- Get the Instance ID

```sh

INSTANCE_ID=$(aws ec2 describe-instances \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=devops-ec2" "Name=instance-state-name,Values=running,stopped,pending,stopping" \
  --query "Reservations[].Instances[].InstanceId" \
  --output text)

```

- Terminate the Instance

```
aws ec2 terminate-instances \
  --region us-east-1 \
  --instance-ids $INSTANCE_ID

```

- Wait for "Terminated" State

```
echo "Waiting for $INSTANCE_ID to reach terminated state..."
aws ec2 wait instance-terminated \
  --region us-east-1 \
  --instance-ids $INSTANCE_ID

echo "Success! The instance devops-ec2 has been terminated."

```
