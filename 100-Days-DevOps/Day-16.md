## Task

-----

Install and Configure Nginx as an LBR

-----

## Solution

```
log into LBR server

ssh loki@stbl01 #password

Install nginx

sudo yum install nginx -y

edit the nginx_conf file

vi /etc/nginx/nginx_conf

insert the following into the http side

upstream app_servers {
server stapp01.stratos.xfusioncorp.com:8089;
server stapp02.stratos.xfusioncorp.com:8089;
server stapp03.stratos.xfusioncorp.com:8089;
}

Restart nginx

systemctl reload nginx
nginx -t
log into any of the serve to find the port 

run the following

vi /etc/http/conf/httpd_config

cat /etc/http/conf/httpd_config | grep Listen







