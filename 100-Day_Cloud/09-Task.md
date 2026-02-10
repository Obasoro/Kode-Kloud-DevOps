## Task

As part of the migration, there were some components created under the AWS account. 
The Nautilus DevOps team created one EC2 instance where they forgot to enable the termination protection which is needed for this instance.

An instance named devops-ec2 already exists in us-east-1 region. Enable termination protection for the same.

## Solution

- Get the Instance-ID

```
  INSTANCE_ID=$(aws ec2 describe-instances --region us-east-1 --filters "Name=tag:Name,Values=devops-ec2" --query "Reservations[*].Instances[*].InstanceId" --output text)

```
``` echo INSTANCE_ID:$INSTANCE_ID ```

- Modify Instance
  
```
aws ec2 modify-instance-attribute --region us-east-1 --instance-id $INSTANCE_ID --disable-api-termination

```
