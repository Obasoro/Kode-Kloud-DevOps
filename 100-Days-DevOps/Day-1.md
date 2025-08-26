## Task

```sh
To accommodate the backup agent tools specifications, the system admin team at xFusion Corp Industries
requires the creation of a user with a non-interactive shell.
Here's your task: Create a user named siva with a non-interactive shell on App Server 3.

```

## Solution
```sh
login into the `stapp03` server

ssh user@server-name
type password

ssh banner@stapp03

password: BigGr33n

```

## Create a non-interactice login

```sh
sudo adduser siva -s /sbin/nologin

grep siva /etc/passwd

```
