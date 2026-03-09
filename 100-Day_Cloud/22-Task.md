## Task

The Nautilus DevOps team needs to set up a new EC2 instance that can be accessed securely from their landing host (aws-client). The instance should be of type t2.micro and named devops-ec2. A new SSH key with name id_rsa should be created on the aws-client host under the/root/.ssh/ folder, if it doesn't already exist. This key should then be added to the root user's authorised keys on the EC2 instance, allowing passwordless SSH access from the aws-client host.


## Solutions

- Generate SSH Keys

```
# Check if key already exists; create only if missing
if [ ! -f /root/.ssh/id_rsa ]; then
    mkdir -p /root/.ssh
    chmod 700 /root/.ssh
    ssh-keygen -t rsa -b 4096 -f /root/.ssh/id_rsa -N "" -C "devops-ec2-access"
    echo "SSH key created."
else
    echo "SSH key already exists, skipping."
fi

# Display the public key (you'll need this shortly)
cat /root/.ssh/id_rsa.pub

```

- Gather AWS Credentials

```
# Get default VPC ID
VPC_ID=$(aws ec2 describe-vpcs \
  --filters "Name=isDefault,Values=true" \
  --query "Vpcs[0].VpcId" \
  --output text)
echo "VPC: $VPC_ID"

# Get a subnet in that VPC
SUBNET_ID=$(aws ec2 describe-subnets \
  --filters "Name=vpc-id,Values=$VPC_ID" \
  --query "Subnets[0].SubnetId" \
  --output text)
echo "Subnet: $SUBNET_ID"

# Get a suitable AMI (Amazon Linux 2 latest)
AMI_ID=$(aws ec2 describe-images \
  --owners amazon \
  --filters "Name=name,Values=amzn2-ami-hvm-*-x86_64-gp2" \
            "Name=state,Values=available" \
  --query "sort_by(Images, &CreationDate)[-1].ImageId" \
  --output text)
echo "AMI: $AMI_ID"

```

- Security Group (allow SSH)

```

SG_ID=$(aws ec2 create-security-group \
  --group-name "devops-ec2-sg" \
  --description "Security group for devops-ec2" \
  --vpc-id "$VPC_ID" \
  --query "GroupId" \
  --output text)
echo "Security Group: $SG_ID"

# Allow SSH (port 22) inbound
aws ec2 authorize-security-group-ingress \
  --group-id "$SG_ID" \
  --protocol tcp \
  --port 22 \
  --cidr 0.0.0.0/0
```

- Import SSH keys into AWS

```
PUBLIC_KEY=$(cat /root/.ssh/id_rsa.pub)

aws ec2 import-key-pair \
  --key-name "devops-ec2-key" \
  --public-key-material fileb:///root/.ssh/id_rsa.pub
echo "Key pair imported."

```

- Launch EC2 Instance

```
INSTANCE_ID=$(aws ec2 run-instances \
  --image-id "$AMI_ID" \
  --instance-type t2.micro \
  --key-name "devops-ec2-key" \
  --security-group-ids "$SG_ID" \
  --subnet-id "$SUBNET_ID" \
  --associate-public-ip-address \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=devops-ec2}]' \
  --query "Instances[0].InstanceId" \
  --output text)
echo "Instance launched: $INSTANCE_ID"

```

- Check for Running Instance

```
echo "Waiting for instance to reach 'running' state..."
aws ec2 wait instance-running --instance-ids "$INSTANCE_ID"

# Get the public IP
PUBLIC_IP=$(aws ec2 describe-instances \
  --instance-ids "$INSTANCE_ID" \
  --query "Reservations[0].Instances[0].PublicIpAddress" \
  --output text)
echo "Instance Public IP: $PUBLIC_IP"

```

- Retrieve Instance ID

```
# Look up the instance by name tag
INSTANCE_ID=$(aws ec2 describe-instances \
  --filters "Name=tag:Name,Values=devops-ec2" \
            "Name=instance-state-name,Values=running" \
  --query "Reservations[0].Instances[0].InstanceId" \
  --output text)
echo "Instance ID: $INSTANCE_ID"

# Get the public IP
PUBLIC_IP=$(aws ec2 describe-instances \
  --instance-ids "$INSTANCE_ID" \
  --query "Reservations[0].Instances[0].PublicIpAddress" \
  --output text)
echo "Public IP: $PUBLIC_IP"

```

- Rerun SSH Config

```
ssh -o StrictHostKeyChecking=no \
    -i /root/.ssh/id_rsa \
    ec2-user@$PUBLIC_IP \
    "sudo mkdir -p /root/.ssh && \
     sudo cp /home/ec2-user/.ssh/authorized_keys /root/.ssh/authorized_keys && \
     sudo chmod 700 /root/.ssh && \
     sudo chmod 600 /root/.ssh/authorized_keys && \
     sudo sed -i 's/^.*PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
     sudo systemctl restart sshd"

echo "Root SSH access configured."

```

- Verify SSH Connection

```
ssh -o StrictHostKeyChecking=no \
    -i /root/.ssh/id_rsa \
    root@$PUBLIC_IP \
    "echo 'Success! Logged in as: \$(whoami) on \$(hostname)'"
```



  
