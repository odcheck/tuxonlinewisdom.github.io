---
title: 'Make Reboot great again'
date: '2019-06-12'
categories: [IT]
tags: [kernel, linux, shutdown, reboot]     # TAG names should always be lowercase
---
Have you ever had such a problem?
<pre>
 # reboot
 bash: /sbin/reboot: Input/output error
 # shutdown -r now
 bash: /sbin/shutdown: Input/output error
 </pre>
>  Obviously, there is a problem with your drive. These commands are failing because the kernel is unable to load the /sbin/reboot and /sbin/shutdown binaries from the disk so that it can execute them.
>  
 At least you could try this
 <pre>echo 1 > /proc/sys/kernel/sysrq</pre>
 and then talk direct to the kernel
 <pre>echo b > /proc/sysrq-trigger</pre>