## Task
- The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the Azure cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

- For this task, create an SSH key pair with the following requirements:

- The name of the SSH key pair should be datacenter-kp.

- The key pair type must be rsa.

## Solution

To List available group if any exit

``az group list --query "[].name" -o tsv```

Input the resource group listed above

```az sshkey create \
  --name datacenter-kp \
  --resource-group <your-resource-group-name> \
  --public-key @~/.ssh/datacenter-kp.pub```
