---
title: 'Port forwarding in Windows'
date: 2021-04-14
categories: [IT]
tags: [win, it, networking]     # TAG names should always be lowercase
---
I've been messing around with Jekyll for a bit and was wondering how I could get port forwarding to work under Windows,  
so that I could access port 4000 gracefully via port 80.

**here we go to start**
```
netsh interface portproxy add v4tov4 listenport=4000 listenaddress=172.29.166.87 connectport=80 connectaddress=192.168.1.115
```
**here we go to delete it again**
```
netsh interface portproxy delete v4tov4 listenport=4000 listenaddress=172.29.166.87
```

