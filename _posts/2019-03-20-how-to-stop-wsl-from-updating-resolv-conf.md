---
title: 'How to stop wsl from updating resolv.conf'
date: 2019-03-20
categories: [IT]
tags: [ubuntu, wsl, dns, microsoft, dhcp-hooks]
---

<p>Currently I'am using Windows 10 Pro Buid 17134.648 and Ubuntu 18.04 within the WSL Bash.</p>
<p>To avoid updating the /etc/resolv.conf wich is a symlink pointing to&nbsp;/run/resolvconf/resolv.conf the default methods like&nbsp;dhclient-enter-hooks.d doesn't work.</p>
<p>Easy way out</p>
<p>Delete /etc/resolv.conf<br />Create a new /etc/resolv.conf&nbsp;<br /><br /><br /><br /></p>