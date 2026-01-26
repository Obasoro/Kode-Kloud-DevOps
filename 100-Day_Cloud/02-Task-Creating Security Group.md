## Task


## Solution
****
# Create the security group
aws ec2 create-security-group \
    --group-name nautilus-sg \
    --description "Security group for Nautilus App Servers"

# Add HTTP rule
aws ec2 authorize-security-group-ingress \
    --group-name nautilus-sg \
    --protocol tcp \
    --port 80 \
    --cidr 0.0.0.0/0

# Add SSH rule
aws ec2 authorize-security-group-ingress \
    --group-name nautilus-sg \
    --protocol tcp \
    --port 22 \
    --cidr 0.0.0.0/0
