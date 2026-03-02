## Task

When establishing infrastructure on the AWS cloud, Identity and Access Management (IAM) is among the first and most critical services to configure. IAM facilitates the creation and management of user accounts, 
groups, roles, policies, and other access controls. The Nautilus DevOps team is currently in the process of configuring these resources and has outlined the following requirements.

Create an IAM policy named iampolicy_john in us-east-1 region, it must allow read-only access to the EC2 console, i.e this policy must allow users to view all instances, AMIs, and snapshots in the Amazon EC2 console.


## Solutions

- Create a Policy

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowEC2ReadOnlyAccess",
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeInstances",
                "ec2:DescribeImages",
                "ec2:DescribeSnapshots",
                "ec2:DescribeTags",
                "ec2:DescribeVolumes",
                "ec2:DescribeKeyPairs"
            ],
            "Resource": "*"
        }
    ]
}

```

- Run the policy within the command line

```
aws iam create-policy \
    --policy-name iampolicy_john \
    --policy-document file://policy.json \
    --description "Read-only access to EC2 instances, AMIs, and snapshots" \
    --region us-east-1

```

- Validate the policy creation

```
aws iam list-policies --scope Local --query 'Policies[?PolicyName==`iampolicy_john`].Arn' --output text

```
