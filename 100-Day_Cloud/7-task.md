## Task
****
During the migration process, the Nautilus DevOps team created several EC2 instances in different regions. 
They are currently in the process of identifying the correct resources and utilization and are making continuous 
changes to ensure optimal resource utilization. Recently, they discovered that one of the EC2 instances was underutilized, 
prompting them to decide to change the instance type. Please make sure the Status check is completed 
(if its still in Initializing state) before making any changes to the instance.

1) Change the instance type from t2.micro to t2.nano for nautilus-ec2 instance.

2) Make sure the ec2 instance nautilus-ec2 is in running state after the change.

## Solution
****

- Retrieve the instance-ID
  ```INSTANCE_ID=$(aws ec2 describe-instances --filters "Name=tag:Name,Values=nautilus-ec2" --query "Reservations[].Instances[].InstanceId" --output text)
echo "Instance ID: $INSTANCE_ID"

```

- Stop the EC2 instance
```
aws ec2 stop-instances --instance-ids "$INSTANCE_ID"

```
- Wait for the instance to enter the 'stopped' state

```sh
aws ec2 wait instance-stopped --instance-ids "$INSTANCE_ID"
echo "Instance stopped."

```

- Change the instance type
  
```
aws ec2 modify-instance-attribute --instance-id "$INSTANCE_ID" --instance-type "{\"Value\": \"t2.nano\"}"
echo "Instance type changed to t2.nano."

```

- Start the EC2 instance

```
aws ec2 start-instances --instance-ids "$INSTANCE_ID"

```

- Verify the instance "Running State"

```sh
aws ec2 wait instance-running --instance-ids "$INSTANCE_ID"
echo "Instance is now running."

aws ec2 describe-instances --instance-ids "$INSTANCE_ID" --query "Reservations[].Instances[].[InstanceId,State.Name,InstanceType]" --output table

```
