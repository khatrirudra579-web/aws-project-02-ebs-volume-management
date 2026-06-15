# AWS Project 02 - EBS Volume Management

## Why This Matters

In production environments, servers frequently run out of storage as applications, logs, and databases grow over time. AWS Elastic Block Store (EBS) allows administrators to dynamically add, resize, and manage storage volumes without rebuilding infrastructure, making it a critical skill for cloud engineers and DevOps professionals.

## Project Overview

This project demonstrates how to create, attach, mount, and manage an AWS EBS volume on an EC2 instance. The goal was to expand server storage and make the volume available for application data.

## Repository Information

**Repository Name:** aws-project-02-ebs-volume-management

**Description:** Hands-on AWS project demonstrating EBS volume creation, attachment, mounting, filesystem creation, and persistent storage management on an EC2 instance.

--

## Architecture

```text
AWS Console
     │
     ▼
Create EBS Volume
     │
     ▼
Attach Volume to EC2 Instance
     │
     ▼
Linux OS Detects New Disk
     │
     ▼
Create Filesystem
     │
     ▼
Mount Volume
     │
     ▼
Persistent Storage Available
```

---

## Prerequisites

* AWS Account
* EC2 Instance (Amazon Linux 2023 / RHEL-based)
* SSH Access
* Basic Linux Command Knowledge

---

## Commands Used

### Check Existing Disks

```bash
lsblk
```

### Create Filesystem on New Volume

```bash
sudo mkfs -t xfs /dev/xvdf
```

### Create Mount Directory

```bash
sudo mkdir /data
```

### Mount Volume

```bash
sudo mount /dev/xvdf /data
```

### Verify Mount

```bash
df -h
```

### Check UUID

```bash
sudo blkid
```

### Configure Persistent Mount

```bash
sudo vi /etc/fstab
```

Example entry:

```text
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx /data xfs defaults,nofail 0 2
```

### Test fstab Configuration

```bash
sudo mount -a
```

---

## Steps Performed

### Step 1: Created an EBS Volume

Created a new EBS volume from the AWS Management Console in the same Availability Zone as the EC2 instance.

Screenshot: `screenshots/screenshot-1-ebs-created.png`

### Step 2: Attached Volume to EC2

Attached the newly created volume to the running EC2 instance as an additional block device.

Screenshot: `screenshots/screenshot-2-volume-attached.png`

### Step 3: Verified Disk Detection

Connected to the server through SSH and confirmed Linux detected the new storage device using:

```bash
lsblk
```

Screenshot: `screenshots/screenshot-3-lsblk-output.png`

### Step 4: Created Filesystem

Formatted the new disk with the XFS filesystem.

```bash
sudo mkfs -t xfs /dev/xvdf
```

Screenshot: `screenshots/screenshot-4-filesystem-created.png`

### Step 5: Mounted the Volume

Created a mount point and mounted the disk.

```bash
sudo mkdir /data
sudo mount /dev/xvdf /data
```

Screenshot: `screenshots/screenshot-5-volume-mounted.png`

### Step 6: Configured Persistent Storage

Retrieved the volume UUID and updated `/etc/fstab` so the volume automatically mounts after server reboot.

Screenshot: `screenshots/screenshot-6-fstab-config.png`

### Step 7: Verified Persistence

Tested configuration using:

```bash
sudo mount -a
df -h
```

Screenshot: `screenshots/screenshot-7-persistent-storage-verified.png`

---

## Challenges Faced & Fixes

### Issue 1: Volume Not Appearing Immediately

**Problem:** Newly attached EBS volume did not show up instantly.

**Fix:** Ran:

```bash
lsblk
```

again after a short wait and verified attachment status in AWS Console.

### Issue 2: Mount Lost After Reboot

**Problem:** Mounted volume disappeared after restarting the instance.

**Fix:** Added the volume UUID to `/etc/fstab` to ensure automatic mounting during boot.

---

## Real-World Use Case

Organizations often attach additional EBS volumes to production servers when application logs, databases, backups, or user-uploaded files require more storage without replacing existing infrastructure.

---

## Skills Learned

* AWS EBS volume provisioning
* EC2 storage expansion
* Linux block device management
* Filesystem creation using XFS
* Mount point configuration
* Persistent storage configuration using `/etc/fstab`
* EBS attachment and lifecycle management
* Storage troubleshooting and verification

---

## Screenshots

```text
screenshots/
├── screenshot-1-ebs-created.png
├── screenshot-2-volume-attached.png
├── screenshot-3-lsblk-output.png
├── screenshot-4-filesystem-created.png
├── screenshot-5-volume-mounted.png
├── screenshot-6-fstab-config.png
└── screenshot-7-persistent-storage-verified.png
```

---

## Project Outcome

Successfully created, attached, formatted, mounted, and configured an AWS EBS volume for persistent storage on an EC2 instance.

---

## Next Steps / What I'd Do Differently

* Experiment with resizing EBS volumes without downtime.
* Explore EBS snapshots for backup and disaster recovery.
* Test different volume types (gp3, io2, st1) and compare performance.
* Automate storage provisioning using Terraform or CloudFormation.
