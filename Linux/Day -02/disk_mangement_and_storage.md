# Storage and Disk Management in Linux (Ubuntu)
 
## 1. Understanding Linux Storage Basics
 
In Linux, every storage device is treated as a file under `/dev`.
 
| Device pattern | Meaning |
|---|---|
| `/dev/sda`, `/dev/sdb` | SATA / SCSI / USB disks |
| `/dev/sda1`, `/dev/sda2` | Partitions on `/dev/sda` |
| `/dev/nvme0n1` | NVMe SSD |
| `/dev/nvme0n1p1` | First partition on NVMe disk |
| `/dev/mapper/...` | LVM logical volumes or LUKS-encrypted devices |
| `/dev/loop0` | Loopback device (e.g., a mounted ISO) |
 
The typical layout is: **physical disk → partition → filesystem → mount point**.
 
---
 
## 2. Viewing Disks and Partitions
 
### `lsblk` — list block devices (the everyday command)
 
```bash
lsblk
```
 
Example output:
 
```
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda      8:0    0   500G  0 disk
├─sda1   8:1    0   512M  0 part /boot/efi
├─sda2   8:2    0     1G  0 part /boot
└─sda3   8:3    0 498.5G  0 part /
sdb      8:16   1    32G  0 disk
└─sdb1   8:17   1    32G  0 part /media/usb
```
 
Useful flags:
 
```bash
lsblk -f          # show filesystem type, UUID, and label
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT,UUID
```
 
### `df` — show mounted filesystem usage
 
```bash
df -h             # human-readable sizes
df -hT            # also show filesystem type
df -i             # show inode usage (useful when "disk full" but space looks free)
```
 
### `du` — show how much space files/directories consume
 
```bash
du -sh /var/log              # total size of one directory
du -h --max-depth=1 /home    # one-level breakdown
du -ah /var | sort -rh | head -20   # top 20 biggest items
```
 
