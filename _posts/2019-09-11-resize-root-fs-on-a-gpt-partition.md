---
title: 'Resize root filesystem on a GPT partition' # Title in the Post as H1
date: 2019-09-11
categories: [IT] # categories
tags: [gdisk, gpt, resize, linux, partition] # always in small letters
---
So, here is how I resized my ext4 root partition (sda2) using gdisk and resize2fs:
```
$ gdisk /dev/sda

Print information (i<enter>2)
Partition GUID code: 0FC63DAF-8483-4772-8E79-3D69D8477DE4 (Linux filesystem)
Partition unique GUID: 7FAC4BC8-6186-4CDF-B6CA-EB73D7C942D1
First sector: 206848 (at 101.0 MiB)
Last sector: 109051903 (at 52.0 GiB)
Partition size: 108845056 sectors (51.9 GiB)
Attribute flags: 0000000000000000
Partition name: ''
Delete the partition (d<enter>2<enter>)
Command (? for help): d
Partition number (1-4): 2
Recreate a new, large partition (n<enter>2<enter>….)
on my setup, gdisk guessed the right first sector. The end sector was also guessed right, since I wanted to fill it up all remaining space
Command (? for help): n
Partition number (2-128, default 2): 
First sector (34-500118158, default = 206848) or {+-}size{KMGTP}: 
Last sector (206848-336072703, default = 336072703) or {+-}size{KMGTP}: 
Current type is 'Linux filesystem'
Hex code or GUID (L to show codes, Enter = 8300): 
Changed type of partition to 'Linux filesystem'
Now copy the old Partition unique GUID to the new partition (x<enter>c<enter>2<enter>)
Command (? for help): x
Expert command (? for help): c

Partition number (1-4): 2
Enter the partition's new unique GUID ('R' to randomize): 7FAC4BC8-6186-4CDF-B6CA-EB73D7C942D1
New GUID is 7FAC4BC8-6186-4CDF-B6CA-EB73D7C942D1
At this point one can verify everything again, after pressing w (to safe the partition), your data might be lost if you did not do this carefully…  
    Just be warned.
```
Reread your block device partition ($ partprobe) 
```
sudo resize2fs /dev/sda2
```

*output*
```
resize2fs 1.42.8 (20-Jun-2013)
Filesystem at /dev/sda2 is mounted on /; on-line resizing required
old_desc_blocks = 4, new_desc_blocks = 11
The filesystem on /dev/sda2 is now 41983232 blocks long.
```
