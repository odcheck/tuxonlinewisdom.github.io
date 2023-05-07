---
title: 'How to Find Directories Larger Than 1GB in Linux'
date: 2018-09-08
categories: [IT]
tags: [disk, usage, du, linux]
---

```
du -h --max-depth=1 / | grep '[0-9]G\>' | sort -hr
```