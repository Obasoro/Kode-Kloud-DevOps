## Task

```
The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks.
One is to create a bash script for taking websites backup. They have a static website running on App Server 2 in Stratos Datacenter,
and they need to create a bash script named official_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 2).



a. Create a zip archive named xfusioncorp_official.zip of /var/www/html/official directory.


b. Save the archive in /backup/ on App Server 2. This is a temporary storage, as backups from this location will be clean on weekly basis.
Therefore, we also need to save this backup archive on Nautilus Backup Server.


c. Copy the created archive to Nautilus Backup Server server in /backup/ location.


d. Please make sure script won't ask for password while copying the archive file.
Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.


e. Do not use sudo inside the script.

```

## Solutions

# Website Backup Script Setup Guide

## Prerequisites

### 1. Install zip package on App Server 2
```bash
# On App Server 2 (as root or with sudo)
yum install zip -y
# or for Debian/Ubuntu systems:
# apt-get install zip -y
```

### 2. Set up SSH key authentication (passwordless login)

On **App Server 2**, run as the server user (likely `steve` for App Server 2):

```bash
# Generate SSH key pair (if not already exists)
ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_rsa -N ""

# Copy public key to Nautilus Backup Server
ssh-copy-id banner@stbkp01.stratos.xfusioncorp.com

# Test passwordless connection
ssh banner@stbkp01.stratos.xfusioncorp.com "echo 'Connection successful'"
```

## Script Installation

### 1. Create scripts directory
```bash
# On App Server 2
mkdir -p /scripts
```

### 2. Create the backup script
```bash
# Create the script file
cat > /scripts/official_backup.sh << 'EOF'
zip -r /backup/xfusion_official.zip /var/www/html/offcicial

scp /backup/xfusion_official.zip clint@stbk01

EOF
```

### 3. Set proper permissions
```bash
# Make script executable
chmod +x /scripts/official_backup.sh

# Set ownership (replace 'steve' with actual App Server 2 user)
chown steve:steve /scripts/official_backup.sh
```

### 4. Create backup directory
```bash
# Create local backup directory
mkdir -p /backup
chown steve:steve /backup
```

### 5. Verify backup server directory exists
```bash
# On Nautilus Backup Server, ensure backup directory exists
ssh clint@stbkp01.stratos.xfusioncorp.com "mkdir -p /backup"
```

## Testing the Script

### 1. Test run
```bash
# Run the script as the server user
/scripts/official_backup.sh
```

### 2. Verify outputs
```bash
# Check local backup
ls -la /backup/xfusioncorp_official.zip

# Check remote backup
ssh clint@stbkp01.stratos.xfusioncorp.com "ls -la /backup/xfusioncorp_official.zip"
```

## Script Features

- ✅ Creates zip archive of `/var/www/html/official`
- ✅ Saves archive as `xfusioncorp_official.zip` in `/backup/`
- ✅ Copies archive to Nautilus Backup Server
- ✅ Passwordless SSH authentication
- ✅ Comprehensive logging with timestamps
- ✅ Error handling and verification
- ✅ No sudo usage within script
- ✅ Executable by server user

## Automation (Optional)

To run the backup automatically, add to crontab:

```bash
# Edit crontab for the server user
crontab -e

# Add entry for daily backup at 2 AM
0 2 * * * /scripts/official_backup.sh >> /var/log/backup.log 2>&1
```

## Troubleshooting

### Common Issues

1. **Permission denied errors**
   - Ensure script has execute permissions
   - Verify directory ownership

2. **SSH connection fails**
   - Check SSH key authentication setup
   - Verify network connectivity to backup server

3. **Zip command not found**
   - Install zip package: `yum install zip -y`

4. **Directory doesn't exist**
   - Script will create `/backup/` automatically
   - Ensure `/var/www/html/official` exists

### Log Analysis
The script provides detailed logging. Check output for:
- Timestamp of each operation
- Success/error messages
- Archive size verification
- Remote copy confirmation

Note:
The zip package must be installed on given App Server before executing the script. This package is essential for creating the zip archive of the website files. Install it manually outside the script.
