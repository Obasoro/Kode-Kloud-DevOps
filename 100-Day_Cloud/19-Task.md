## Task




## Solution

```

# Get the ARN automatically into a variable
POLICY_ARN=$(aws iam list-policies --scope Local --query 'Policies[?PolicyName==`iampolicy_john`].Arn' --output text)

# Attach it to the user
aws iam attach-user-policy \
    --user-name iamuser_john \
    --policy-arn $POLICY_ARN \
    --region us-east-1

```

- Validate the Policy attachment

```
aws iam list-attached-user-policies --user-name iamuser_john

```
