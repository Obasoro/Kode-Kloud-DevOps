## Task

When establishing infrastructure on the AWS cloud, Identity and Access Management (IAM) is among the first and most critical services to configure. IAM facilitates the creation and management of user accounts, groups, roles, policies, and other access controls. The Nautilus DevOps team is currently in the process of configuring these resources and has outlined the following requirements:

Create an IAM role as below:

1) IAM role name must be iamrole_anita.

2) Entity type must be AWS Service and use case must be EC2.

3) Attach a policy named iampolicy_anita.


## Solution

1) Create a Policy `trust-policy`

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}

```

2) Create the IAM rol

```
aws iam create-role \
    --role-name iamrole_anita \
    --assume-role-policy-document file://trust-policy.json
```

3) Get the ARN of your existing policy 'iampolicy_anita'

```
POLICY_ARN=$(aws iam list-policies --scope Local --query 'Policies[?PolicyName==`iampolicy_anita`].Arn' --output text)

```
4) Attach the policy to the new role

``` aws iam attach-role-policy \
    --role-name iamrole_anita \
    --policy-arn $POLICY_ARN

```

5) Verify Configuration

```
aws iam get-role --role-name iamrole_anita
aws iam list-attached-role-policies --role-name iamrole_anita
```
