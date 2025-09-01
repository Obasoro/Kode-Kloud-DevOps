## Task

`
Following a security audit, the xFusionCorp Industries security team has opted to enhance application 
and server security with SELinux. To initiate testing, the following requirements have been established 
for App server 3 in the Stratos Datacenter:

[ ] Install the required SELinux packages.

[ ] Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.

[ ] No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.

[ ] Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled

`

## Solotion

### Install Selinux

```ssh banner@stapp03```

`sudo yum install -y policycoreutils selinux-policy`

check for status

sudo sed -i 's/^SELINUX=.*$/SELINUX=disabled/' /etc/selinux/config

or

sudo vi /etc/selinux/config | grep SELINUX

change the `enforcing` to `disabled`

```
