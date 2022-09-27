# Question and Task
The System admin team of xFusionCorp Industries has installed a backup agent tool on all app servers. As per the tool's requirements they need to create a user with a non-interactive shell.

Therefore, create a user named javed with a non-interactive shell on the App Server 

## Step 1

1. ssh into the server given
2. type in the password given for that server
3.create a user either using root privileges or sudo

ssh <username>@server-name or ip
ssh steve@stapp02

***********************************
Input the password
***********************************

sudo useradd user -s /sbin/nologin
or 
sudo su -
useradd user -s /sbin/nologin

sudo useradd javed -s /sbin/nologin


***********************************



To check if the IP has been created 

sudo id user

sudo id javed
  
cat /etc/passwd | grep javed

exit




