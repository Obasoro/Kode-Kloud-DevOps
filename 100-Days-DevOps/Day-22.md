## Task
```
The DevOps team established a new Git repository last week, which remains unused at present.
However, the Nautilus application development team now requires a copy of this repository on the Storage Server in the Stratos DC.
Follow the provided details to clone the repository:
1. The repository to be cloned is located at /opt/media.git
2. Clone this Git repository to the /usr/src/kodekloudrepos directory.
Perform this task using the natasha user, and ensure that no modifications are made to the repository or existing directories,
such as changing permissions or making unauthorized alterations.

```



## Solutions

# Step 1: Switch to the natasha user (if not already logged in as natasha)
# You can either log in directly as natasha or switch user
sudo su - natasha

# Step 2: Navigate to the parent directory and create the target directory if it doesn't exist
sudo mkdir -p /usr/src/kodekloudrepos

# Step 3: Change ownership of the target directory to natasha user (if needed)
sudo chown natasha:natasha /usr/src/kodekloudrepos

# Step 4: Navigate to the target directory
cd /usr/src/kodekloudrepos

# Step 5: Clone the repository from the source location
git clone /opt/media.git

# Alternative: If you want to specify the destination directory name explicitly
# git clone /opt/media.git media

# Step 6: Verify the clone operation was successful
ls -la /usr/src/kodekloudrepos

# Step 7: Check the cloned repository contents
cd media  # or whatever the cloned directory is named
git status
git log --oneline -5  # Show last 5 commits to verify
