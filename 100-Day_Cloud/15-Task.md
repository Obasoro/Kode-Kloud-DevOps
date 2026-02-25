## Task
The Nautilus DevOps team has some volumes in different regions in their AWS account. 
They are going to setup some automated backups so that all important data can be backed up on regular basis. 
For now they shared some requirements to take a snapshot of one of the volumes they have.

Create a snapshot of an existing volume named datacenter-vol in us-east-1 region.

1) The name of the snapshot must be datacenter-vol-ss.

2) The description must be datacenter Snapshot.

3) Make sure the snapshot status is completed before submitting the task.


## Solution

- Get Volume ID

```
VOL_ID=$(aws ec2 describe-volumes \
    --region us-east-1 \
    --filters "Name=tag:Name,Values=datacenter-vol" \
    --query "Volumes[0].VolumeId" \
    --output text)
```

- Create Snapshot

```
SNAP_ID=$(aws ec2 create-snapshot \
    --region us-east-1 \
    --volume-id $VOL_ID \
    --description "datacenter Snapshot" \
    --tag-specifications 'ResourceType=snapshot,Tags=[{Key=Name,Value=datacenter-vol-ss}]' \
    --query "SnapshotId" \
    --output text)

echo "Snapshot created with ID: $SNAP_ID"

```

- Verify Snapshaot creation

```
aws ec2 describe-snapshots \
    --region us-east-1 \
    --snapshot-ids $SNAP_ID \
    --query "Snapshots[0].{ID:SnapshotId,Status:State,Name:Tags[?Key=='Name'].Value|[0]}"

```
