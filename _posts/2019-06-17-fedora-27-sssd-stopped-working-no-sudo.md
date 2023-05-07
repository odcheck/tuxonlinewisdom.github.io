---
title: 'Fedora 27 sssd stopped working "no sudo anymore"'
date: 2019-06-17
categories: [IT]
tags: [fedora, sssd, sudo]
---
> sudo: unable to load /usr/lib64/libsss_sudo.so: /usr/lib64/libsss_sudo.so: cannot open shared object file: No such file or directory
> 

**Reason:** ? Maybe due an Update it got broken. \
**Solution:** 
```
yum -y install libsss_sudo
```
