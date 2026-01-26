## Task 2


## Solution

```
az group list --query "[].name"

```

```
az vm create \
  --resource-group kml_rg_main-ad4ad99dd9b8439b \
  --name devops-vm \
  --location centralus \
  --image Ubuntu2204 \
  --size Standard_B1s \
  --admin-username azureuser \
  --generate-ssh-keys \
  --public-ip-sku Standard \
  --nsg-rule SSH \
  --os-disk-size-gb 64 \
  --storage-sku Standard_LRS
```
