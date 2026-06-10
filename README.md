# AWS Project 02 - EBS Volume Management

## Project Overview

This project demonstrates how to create, attach, format, mount, and persist an Amazon EBS volume on an EC2 instance.

## Services Used

- Amazon EC2
- Amazon EBS
- EBS Snapshots

## Skills Learned

- EBS Volume Creation
- Volume Attachment
- Linux Disk Management
- XFS Filesystem Creation
- Mounting Storage
- Persistent Mounts with /etc/fstab
- Snapshot Backups
- Linux Troubleshooting

## Architecture

EC2 Instance
|
└── EBS Volume (10 GB)
|
└── Mounted at /data

## Commands Used

See:

commands/setup-commands.txt

## Screenshots

Available in:

screenshots/

## Key Learning

A typo in the UUID inside /etc/fstab prevented the volume from mounting automatically. Troubleshooting and correcting the UUID restored functionality.

## What a Junior DevOps Engineer Should Be Able to Explain

- Difference between EC2 and EBS
- What a filesystem is
- How Linux mounts storage
- Purpose of /etc/fstab
- Why UUIDs are used instead of device names
- How EBS snapshots help with disaster recovery