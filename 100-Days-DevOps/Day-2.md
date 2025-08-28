## Task
```sh
As part of the temporary assignment to the Nautilus project,
a developer named javed requires access for a limited duration. To ensure smooth access management,
a temporary user account with an expiry date is needed. Here's what you need to do:

Create a user named javed on App Server 1 in Stratos Datacenter.
Set the expiry date to 2024-04-15, ensuring the user is created in lowercase as per standard protocol.
```

## Solution

You can create `javed' user directly by using sudo or enter as a root user.

### Creation of User

```sh

sudo adduser -M javed

sudo su -

adduser -M javed

```
### Change of Expiring Date

check the expiration date `chage -l username` or `chage -help` to see how to change expiry date of users

```
 chage -help
Usage: chage [options] LOGIN

Options:
  -d, --lastday LAST_DAY        set date of last password change to LAST_DAY
  -E, --expiredate EXPIRE_DATE  set account expiration date to EXPIRE_DATE
  -h, --help                    display this help message and exit
  -i, --iso8601                 use YYYY-MM-DD when printing dates
  -I, --inactive INACTIVE       set password inactive after expiration
                                to INACTIVE
  -l, --list                    show account aging information
  -m, --mindays MIN_DAYS        set minimum number of days before password
                                change to MIN_DAYS
  -M, --maxdays MAX_DAYS        set maximum number of days before password
                                change to MAX_DAYS
  -R, --root CHROOT_DIR         directory to chroot into
  -W, --warndays WARN_DAYS      set expiration warning days to WARN_DAYS

``

```chage -E YYYY-M-D username```



 
 
 
