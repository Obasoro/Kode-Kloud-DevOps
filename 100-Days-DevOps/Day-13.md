## Task

```
We have one of our websites up and running on our Nautilus infrastructure in Stratos DC.
Our security team has raised a concern that right now Apache’s port i.e 8083 is open for all since there is no firewall installed on
these hosts. So we have decided to add some security layer for these hosts and after discussions and recommendations
we have come up with the following requirements:

1. Install iptables and all its dependencies on each app host.


2. Block incoming port 8083 on all apps for everyone except for LBR host.


3. Make sure the rules remain, even after system reboot.

```

## Solution

```sh

ssh tony@stapp01

 yum install  -y iptables-services

systemctl start iptables && systemctl enable iptables

iptables -A INPUT -p tcp --destination-port 8081 -s 172.16.238.14 -j ACCEPT
iptables -A INPUT -p tcp --destination-port 8081 -j DROP

iptables -L --line-numbers

iptables -R INPUT 5 -p icmp -j REJECT

service iptables save

systemctl restart iptables && systemctl status iptables
