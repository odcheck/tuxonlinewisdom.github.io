---
title: 'Journalctl clean up and tricks'
date: 2019-09-22
categories: [IT]
tags: [journals, logfiles, linux]
---
**Find the current Disk Usage by journalctl**
```
journalctl --disk-usage
```

**The safest way to remove unessesary entries is via the (means leave this amount left)**
```
journalctl --vacuum-size=512M
```

**After that you can verify if everything is still intact:**
```
journalctl --verify
```

**Or as generell setting in /etc/systemd/journald.conf**
```
SystemMaxUse=512M
```

*different approach:*
```
SystemMaxFileSize=12M
SystemMaxFiles=10
```
