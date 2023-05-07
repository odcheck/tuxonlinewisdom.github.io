---
title: 'Requested operation is not valid: cannot set autostart for transient network'
date: 2019-12-23
categories: [IT]
tags: [linux, kvm, network, libvirt, transient, autostart]
---
virsh net-autostart networkname leads to the above mentioned Error Message.
The solution is stupid but it works...

```
virsh net-edit networkname
```
go to the end and add some empty lines, save the file and quit.

```
virsh net-autostart networkname
```
works like charm....
