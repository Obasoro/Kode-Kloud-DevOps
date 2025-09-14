## Task

-----------------

Install of LAMP stack on Server

---------------

## Solutions

```
ssh tony@stapp01 #password

Install the Apache and Php dependencies

dnf install php php-opcache php-gd php-curl php-mysqlnd -y
dnf install httpd -y
systemctl start httpd
systemctl status httpd
systemctl start php-fpm <-- FactCGI Process Manager
systemctl status php-fpm

`Repeat for all Servers`

```
### Step 2

Log into Database server 

```ssh peter@stdb01 #password

dnf install mariadb mariadb-server -y
systemctl enable mariadb
systemctl status mariadb
systemctl restart mariadb

sudo -u root mysql;
create database database-name;
create user 'database-user';
GRANT ALL PRIVILEGES ON Database-name.* TO 'database-user'@'%' identified by 'password';
select user,host from mysql.user;

```

### Step 3

Change the `PORT` on the Apache server

`vi /etc/httpd/conf/httpd.conf`



