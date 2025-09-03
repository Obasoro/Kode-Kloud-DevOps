## Task

```
There is a critical issue going on with the Nautilus application in Stratos DC.
The production support team identified that the application is unable to connect to the database.
After digging into the issue, the team found that mariadb service is down on the database server.

Look into the issue and fix the same.

```

## Solutions

The solutions varies but start with checking if the mariadb is active and running

```sduo systemctl start mariadb.service```

If it comes with this error below

<img width="691" height="66" alt="Screenshot 2025-09-03 150501" src="https://github.com/user-attachments/assets/159359e6-bae6-418e-a872-eaf2a95dc3b4" />

or

```sh
2025-09-03 14:24:08 0 [Note] Plugin 'FEEDBACK' is disabled.
2025-09-03 14:24:08 0 [ERROR] Could not open mysql.plugin table: "Table 'mysql.plugin' doesn't exist". Some plugins may be not loaded
2025-09-03 14:24:08 0 [ERROR] Failed to initialize plugins.
2025-09-03 14:24:08 0 [ERROR] Aborting

or

Sep 03 14:24:08 stdb01.stratos.xfusioncorp.com mariadbd[3542]: 2025-09-03 14:24:08 0 [Warning]
Can't create test file '/var/lib/mysql/stdb01.lower-test' (Errcode: 13 "Permission denied")

```

# MariaDB Data Directory Fix Guide

## Problem
The `/var/lib/mysql/` directory doesn't exist, causing MariaDB to fail with:
- Permission denied errors
- Missing plugin table errors
- Server startup failures

## Solution: Create and Initialize MariaDB Data Directory

### 1. Create the Data Directory
```bash
sudo mkdir -p /var/lib/mysql
```

### 2. Set Proper Ownership and Permissions
```bash
sudo chown mysql:mysql /var/lib/mysql
sudo chmod 755 /var/lib/mysql
```

### 3. Initialize MariaDB System Tables
```bash
# Initialize the MariaDB data directory with system tables
sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
```

### 4. Start MariaDB Service
```bash
sudo systemctl start mariadb
sudo systemctl status mariadb
```

### 5. Secure the Installation (Optional but Recommended)
```bash
sudo mysql_secure_installation
```

## Alternative: Check Configuration First

Before proceeding, you might want to verify where MariaDB expects its data directory:

### Check MariaDB Configuration
```bash
# Check MariaDB configuration files
sudo grep -r datadir /etc/mysql/ 2>/dev/null

# Check what the service is configured to use
mysqld --help --verbose 2>/dev/null | grep datadir
```

> **Note:** If the configuration shows a different path than `/var/lib/mysql/`, create the directory at that location instead.

## Troubleshooting

### If You Get Permission Errors During Initialization

Make sure the `mysql` user exists:

```bash
# Check if mysql user exists
getent passwd mysql

# If not, create it
sudo useradd -r -d /var/lib/mysql -s /bin/false mysql
```

### Verify Success

After completing the steps, verify MariaDB is running:

```bash
sudo systemctl status mariadb
sudo mysql -u root -p -e "SELECT VERSION();"
```

## Why This Happens

The missing directory typically occurs when:
- Fresh MariaDB installation wasn't properly initialized
- Data directory was accidentally deleted
- Incorrect configuration pointing to non-existent path
- Package installation didn't complete properly

## Next Steps

After MariaDB is running, consider:
- Setting up regular backups
- Creating application-specific databases and users
- Configuring performance settings based on your use case

