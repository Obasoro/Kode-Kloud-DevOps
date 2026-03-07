## Task
The Nautilus DevOps Team has received a new request from the Development Team to set up a new EC2 instance. This instance will be used to host a new application that requires a stable IP address. To ensure that the instance has a consistent public IP, an Elastic IP address needs to be associated with it. The instance will be named datacenter-ec2, and the Elastic IP will be named datacenter-eip. This setup will help the Development Team to have a reliable and consistent access point for their application.

Create an EC2 instance named datacenter-ec2 using any linux AMI like ubuntu, the Instance type must be t2.micro and associate an Elastic IP address with this instance, name it as datacenter-eip.

## Solution

- Generate the `ami` for the Instance

```

aws ssm get-parameter \
    --name /aws/service/canonical/ubuntu/server/noble/stable/current/amd64/hvm/ebs-gp3/ami-id \
    --query "Parameter.Value" \
    --output text \
    --region us-east-1

```

- Create the Instance

```
# Launch the instance
aws ec2 run-instances \
    --image-id ami-0e2c8ccd4e1ff313c \
    --count 1 \
    --instance-type t2.micro \
    --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=datacenter-ec2}]' \
    --region us-east-1
```

- Associate the Elastic IP

```
# Allocate the IP
ALLOCATION_ID=$(aws ec2 allocate-address \
    --domain vpc \
    --tag-specifications 'ResourceType=elastic-ip,Tags=[{Key=Name,Value=datacenter-eip}]' \
    --query 'AllocationId' \
    --output text \
    --region us-east-1)

echo "Allocation ID: $ALLOCATION_ID"```

Assocoiate the IP

``` aws ec2 associate-address \
    --instance-id YOUR_INSTANCE_ID \
    --allocation-id $ALLOCATION_ID \
    --region us-east-1

```
