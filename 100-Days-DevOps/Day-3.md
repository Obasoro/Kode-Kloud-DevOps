## Task
```
Following security audits, the xFusionCorp Industries security team has rolled out new protocols,
including the restriction of direct root SSH login

```

## Solutions

```sh
ssh tony@stapp01 #password:Ir0nM@n

ssh banner@stapp02 #password:BigGr33n

ssh steve@stapp03 #passowrd:Am3ric@

```

`sudo vi /etc/ssh/sshd_config` change the `PermitRootLogin` from `yes` to `no`

### Restart ssh

`sudo systemctl restart sshd`

Repeat for the servers and you are Good.
