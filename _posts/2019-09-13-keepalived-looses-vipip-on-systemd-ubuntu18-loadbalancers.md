---
title: 'keepalived looses VIP IP on systemd Ubuntu18 (Loadbalancers)'
date: 2019-09-22
categories: [IT]
tags: [keepalived, lb, vip, ubuntu]
---

Version pre 2.x of keepalive which are shipped with the Ubuntu18 Repository will crash.
You'll have to configure a higher Version from source by yourself.

[https://github.com/acassen/keepalived/issues/836](https://github.com/acassen/keepalived/issues/836){:target="_blank"}

[https://www.keepalived.org/download.html](https://www.keepalived.org/download.html){:target="_blank"}

"/lib/systemd/system/keepalived.service"

```
[Unit]
Description=LVS and VRRP High Availability Monitor
After=network-online.target syslog.target
Wants=network-online.target

[Service]
Type=forking
PIDFile=/run/keepalived.pid
KillMode=process
EnvironmentFile=-/usr/local/etc/sysconfig/keepalived
ExecStart=/usr/local/sbin/keepalived $KEEPALIVED_OPTIONS
ExecReload=/bin/kill -HUP $MAINPID

[Install]
WantedBy=multi-user.target
```