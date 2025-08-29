## Task
```sh
In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh.
While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 1 within the Stratos Datacenter.

Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 1.
Additionally, ensure that all users have the capability to execute it.

```

## Solution

```sh

ssh tony@stapp01 #use password

I tried sudo chmod u+x /tmp/xfusioncorp.sh  permission for user only for execution

sudo chmod o+rx /tmp/xfusioncorp.sh gaves other who are not the user to execute.

```
