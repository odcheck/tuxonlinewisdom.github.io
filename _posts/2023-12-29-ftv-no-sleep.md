---
title: 'No sleep till brooklyn for Amazon Fire TV stick'
date: 2023-12-29
categories: [IT]
tags: [amazon, firetv, adb]
---
1. enable debugging in the settings of your fire tv stick
2. get a adb connection tool and connect using the ip address to your fire tv stick
3. set this values using the following commands
4. i don't care about my grammar and so on 

```
settings put system screen_off_timeout 2147460000
settings put secure sleep_timeout 0
```


