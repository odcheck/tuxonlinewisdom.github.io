---
title: 'Hotplug Memory in running Kvm VM'
date: 2019-03-12 # yyyy-mo-day
categories: [IT]
tags: [virsh, kvm, hotplug, linux]     # TAG names should always be lowercase
---
Easy as this
```
virsh setmem <vmdomname> 4096M --live --config
```



