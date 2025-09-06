## Task

```
Our monitoring tool has reported an issue in Stratos Datacenter. One of our app servers has an issue,
 as its Apache service is not reachable on port 6200 (which is the Apache port).
The service itself could be down, the firewall could be at fault, or something else could be causing the issue.



Use tools like telnet, netstat, etc. to find and fix the issue. Also make sure Apache is reachable
from the jump host without compromising any security settings.

Once fixed, you can test the same using command curl http://stapp01:6200 command from jump host.

Note: Please do not try to alter the existing index.html code, as it will lead to task failure

```

## Solutions

```sh

`on jumphost`

`telnet stapp01 8088`

`ssh tony@stapp01 #password`

`systemctl status httpd` `start,restart,enabled` can be used

`netstat -tulnp`

`ps -ef | grep [PID Number]`

`kill -9 [PID numer]`

`vi /etc/httpd/conf/httpd.conf`

[Uncomment the ServerName in the config file and input the IP with the port]

`netstat -anp |grep LISTEN |grep ":PORT"`

`systemctl restart httpd`
`systemctl status httpd`

`iptables -I INPUT -p tcp -m tcp --dport 8081 -j ACCEPT  && iptables-save > /etc/sysconfig/iptables &&  cat /etc/sysconfig/iptables`

[Idea for the solution](https://gist.github.com/AbdullahGhani1/d7931953358c5599b7ab7ced3f90dad2)

