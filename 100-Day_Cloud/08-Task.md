## Task






## Solutions

- Check the Instance-ID

```
INSTANCE_ID=$(aws ec2 describe-instances --filters "Name=tag:Name,Values=nautilus-ec2" --query "Reservations[].Instances[].InstanceId" --output text)
echo "Instance ID: $INSTANCE_ID"

```

- Initiate the Enable Stop Protection for EC2 Instance

```
aws ec2 modify-instance-attribute --instance-id <instance-id> --disable-api-stop '{"Value": true}'

```
