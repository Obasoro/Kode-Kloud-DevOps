## Task 

```
During the weekly meeting, the Nautilus DevOps team discussed about the automation 
and configuration management solutions that they want to implement. 
While considering several options, the team has decided to go with 
Ansible for now due to its simple setup and minimal pre-requisites. 
The team wanted to start testing using Ansible, so they have decided 
to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.



Install ansible version 4.8.0 on Jump host using pip3 only. 
Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.

```

## Solutions

```sh
# Complete Installation Guide for CentOS Jump Host
# Python 3 → pip3 → Ansible 4.10.0
# Nautilus DevOps Team

# STEP 1: Check current system status
echo "=== System Information ==="
cat /etc/os-release
uname -a

# STEP 2: Update system packages
echo "=== Updating system packages ==="
sudo yum update -y

# STEP 3: Install Python 3 (if not already installed)
echo "=== Installing Python 3 ==="
sudo yum install python3 -y

# STEP 4: Verify Python 3 installation
echo "=== Verifying Python 3 ==="
python3 --version
which python3

# STEP 5: Install pip3
echo "=== Installing pip3 ==="
sudo yum install python3-pip -y

# STEP 6: Verify pip3 installation
echo "=== Verifying pip3 installation ==="
pip3 --version
which pip3

# STEP 7: Upgrade pip3 to latest version
echo "=== Upgrading pip3 ==="
sudo python3 -m pip install --upgrade pip

# STEP 8: Fix PATH issue (add /usr/local/bin to global PATH)
echo "=== Configuring global PATH ==="
echo 'export PATH="/usr/local/bin:$PATH"' | sudo tee -a /etc/profile
source /etc/profile

# STEP 9: Verify pip3 is working with updated PATH
echo "=== Testing pip3 functionality ==="
pip3 --version
which pip3

# STEP 10: Install Ansible 4.10.0 globally
echo "=== Installing Ansible 4.10.0 ==="
sudo /usr/local/bin/pip3 install ansible==4.10.0

# STEP 11: Verify Ansible installation
echo "=== Verifying Ansible installation ==="
ansible --version
which ansible

# STEP 12: Check if ansible binaries are in correct location
echo "=== Checking ansible binary locations ==="
ls -la /usr/local/bin/ansible*

# STEP 13: Test global accessibility for all users
echo "=== Testing global accessibility ==="
echo "Testing as thor user:"
ansible --version

echo "Testing as root user:"
sudo ansible --version

echo "Testing by switching to root:"
sudo su - root -c "ansible --version"

# STEP 14: Basic functionality test
echo "=== Testing Ansible functionality ==="
ansible localhost -m ping

# STEP 15: Verify ansible modules are available
echo "=== Checking available modules ==="
ansible-doc -l | head -5

# STEP 16: Verify ansible-playbook is available
echo "=== Checking ansible-playbook ==="
ansible-playbook --version
which ansible-playbook

# STEP 17: Final verification - check specific version
echo "=== Final version verification ==="
pip3 show ansible | grep Version

echo "=== Installation Summary ==="
echo "Python 3: $(python3 --version)"
echo "pip3: $(pip3 --version)"
echo "Ansible location: $(which ansible)"
echo "Ansible version: $(ansible --version | head -1)"
echo "Installation complete!"

```
