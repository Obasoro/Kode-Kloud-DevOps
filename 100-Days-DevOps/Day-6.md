## Task 

```
The Nautilus system admins team has prepared scripts to automate several day-to-day tasks.
They want them to be deployed on all app servers in Stratos DC on a set schedule.
Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:

a. Install cronie package on all Nautilus app servers and start crond service.


b. Add a cron */5 * * * * echo hello > /tmp/cron_text for root user.

```

## Solution

```sh

ssh into all the server

install `cronie` either as `sudo` user or `root` user

run `sudo` systemctl start crond.service

run `sudo` systemctl status crond.service

run `crontab -e` and input the schedule job instruction





