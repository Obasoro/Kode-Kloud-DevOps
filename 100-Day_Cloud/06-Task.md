## Task
The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud.
Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single 
massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units.

For this task, create an EC2 instance with following requirements:

1) The name of the instance must be devops-ec2.

2) You can use the Amazon Linux AMI to launch this instance.

3) The Instance type must be t2.micro.

4) Create a new RSA key pair named devops-kp.

5) Attach the default (available by default) security group.


## Solution

- List the default security Group

 ```aws ec2 describe-security-groups --filters Name=group-name,Values=default```

- Create the key-pair

```aws ec2 create-key-pair --key-name devops-kp --query 'KeyMaterial' --output text > devops-kp.pem ```

- Search for ami id within the region

```
aws ssm get-parameters --names /aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64 --region us-east-1 --query 'Parameters[0].Value' --output text

```

- Create the EC2 instance

```
aws ec2 run-instances \
    --image-id <ami-id> \
    --count 1 \
    --instance-type t2.micro \
    --key-name devops-kp \
    --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=devops-ec2}]'

```
