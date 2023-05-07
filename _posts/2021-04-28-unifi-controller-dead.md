---
title: 'The UniFi Controller 6.1.71 died with a Java Error'
date: 2021-04-28
categories: [IT]
tags: [unifi, controller, dead, raspberry, linux, debian, buster]     # TAG names should always be lowercase
---

## What I did before
I imaged the raspberry Pi with an minimal debian 10 32 bit, then I used this cool installer I have found in the world wide web.

https://community.ui.com/questions/UniFi-Installation-Scripts-or-UniFi-Easy-Update-Script-or-UniFi-Lets-Encrypt-or-UniFi-Easy-Encrypt-/ccbc7530-dd61-40a7-82ec-22b17f027776

**6.1.71 died with** 
```
2021-04-28 18:02:11,486 main ERROR Error processing element InMemoryAppender ([Appenders: null]): CLASS_NOT_FOUND
2021-04-28 18:02:12,662 main ERROR Unable to locate appender "InMemoryAppender" for logger config "root"
```

## What I did then?
I just upgraded using the same script mentioned above to a release canidate Version 6.2.17.




